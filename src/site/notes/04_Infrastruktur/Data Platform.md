---
{"dg-publish":true,"permalink":"/04-infrastruktur/data-platform/","dgPassFrontmatter":true,"noteIcon":"","created":"2025-12-08T19:25:32.186+01:00","updated":"2025-12-13T14:41:39.196+01:00"}
---

# Data Platform Architecture

> Als Data-Driven Community unterscheiden wir uns durch Fakten von "Bauchgefühl"-Clans. Wir bauen eine schlanke, aber skalierbare Datenplattform auf.

## Strategie: "Community Intelligence"

Wir nutzen das **Medallion Architecture Pattern** (Bronze -> Silver -> Gold), angepasst an unsere Scale.

### 1. Stack Overview

| Komponente        | Technologie                      | Warum?                                                         |
| :---------------- | :------------------------------- | :------------------------------------------------------------- |
| **Ingestion**     | Python (Discord.py, RCON)        | Flexibel, direkte API-Anbindung.                               |
| **Orchestration** | Dagster (oder Airflow)           | Da du Data Engineer bist: Sauberer State, Backfills möglich.   |
| **Storage**       | PostgreSQL + TimescaleDB         | Relational für User-Daten, Time-Series für Voice/Server-Stats. |
| **Visualization** | Grafana (Ops) / Metabase (Biz)   | Grafana für Server-Health, Metabase für Community-KPIs.        |
| **Hosting**       | Docker Compose (auf Root-Server) | Einfaches Deployment, alles in Containern.                     |

### 2. Data Flow (Medallion)

#### 🥉 Bronze (Raw Ingestion)
*Ziel: Rohdaten unverändert speichern.*
- **Discord Events:** Raw JSON von Message/Voice Events (via Bot Webhooks oder Polling).
- **Game Server Logs:** Logfiles (CS2, Minecraft) via SFTP oder direktem Mount in `_raw` Tables.
- **Website/Forum:** Access Logs.

#### 🥈 Silver (Refined & Cleaned)
*Ziel: Deduplizierung, Typisierung, Anreicherung.*
- **Dim_User:** Zentrale User-Tabelle (Discord ID + Game IDs gemappt).
- **Fact_Voice_Sessions:** Wer war wann wie lange in welchem Channel? (Start/End Timestamps).
- **Fact_Game_Sessions:** Wer hat wann auf welchem Server gespielt?
- **Dim_Events:** Kalender-Events mit Teilnehmerlisten.

#### 🥇 Gold (Aggregated Business Logic)
*Ziel: Report-Ready KPIs.*
- **Daily_Active_Users (DAU):** Unique Users in Voice + Chat + Game Server.
- **Retention_Cohorts:** Wie viele Neuzugänge aus Monat X sind in Monat X+3 noch aktiv?
- **Server_Utilization:** Auslastung der Game-Server über den Tag (für Cost-Optimization).

## Implementation Details: KPI Tracking

> Wie wir die Metriken technisch erfassen.

### 1. Discord Tracking (Bot Logic)
Wir schreiben einen eigenen Bot (Python/`discord.py`), da Public Bots oft Datenhoheit-Probleme haben.

**A. Voice Session Tracking**
*   **Event:** `on_voice_state_update(member, before, after)`
*   **Logic:**
    *   Wenn `before.channel` is None & `after.channel` is not None -> **JOIN** (Timestamp speichern).
    *   Wenn `before.channel` is not None & `after.channel` is None -> **LEAVE** (Dauer berechnen: `Now - Join_Time`, in DB schreiben).
    *   *Edge Case:* User wechselt Channel -> Session A schließen, Session B starten.
    *   *AFK-Check:* Wenn `after.channel.id == AFK_CHANNEL_ID` -> Nicht als "Active Time" werten.

**B. Chat Activity / DAU**
*   **Event:** `on_message(message)`
*   **Logic:**
    *   `INSERT INTO raw_messages (user_id, channel_id, timestamp, char_count)`
    *   *Privacy:* Wir speichern **NICHT** den Inhalt der Nachricht, nur Metadaten!
    *   **DAU-Calculation:** `SELECT COUNT(DISTINCT user_id) FROM raw_messages WHERE date = CURRENT_DATE`.

**C. Retention Tracking (SQL)**
*   Wir brauchen eine `members` Tabelle mit `join_date`.
*   **Query:**
    ```sql
    WITH cohort AS (
      SELECT user_id FROM members WHERE join_date BETWEEN '2025-01-01' AND '2025-01-31'
    )
    SELECT
      COUNT(DISTINCT t.user_id) as active_month_1
    FROM transactions t
    JOIN cohort c ON t.user_id = c.user_id
    WHERE t.timestamp BETWEEN '2025-02-01' AND '2025-02-28'
    ```

### 2. Game Server Tracking

**A. Source / CS2 (RCON)**
*   **Tool:** Python Script mit `python-valve` Lib.
*   **Frequenz:** Cronjob alle 5 Minuten.
*   **Command:** `status` oder `users`.
*   **Parsing:** Regex über den Output, um SteamIDs und Playtime zu extrahieren.
*   **Store:** `game_sessions` Tabelle (ServerID, SteamID, SnapshotTime).

**B. Minecraft / Andere**
*   **Plugin:** Nutzung von Prometheus Exportern (z.B. "Prometheus Exporter" Plugin für Minecraft).
*   **Ingest:** Prometheus scrapt den Server -> Grafana visualisiert Live-Daten -> ETL-Job aggregiert für Long-Term Stats in Postgres.

## Implementation Roadmap

1.  [ ] **Infrastructure:** Postgres & Grafana via Docker Compose aufsetzen.
2.  [ ] **Discord Bot "Observer":** Ein Bot, der nur Events lauscht und in DB schreibt (keine User-Interaktion).
3.  [ ] **RCON Scraper:** Script, das alle 5 Min `status` vom Game-Server holt und speichert.
4.  [ ] **Dashboard V1:** "Live Activity" Dashboard für Admins.

Weiterführend: [[02_Ziele/KPI Definitions\|KPI Definitions]]

↩ [[Home\|Home]]
