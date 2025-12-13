---
{"dg-publish":true,"permalink":"/05-phasenplan/phase-1-infrastructure-build/"}
---


# Phase 1 – Infrastructure Buildout

**Ziele:** Technische Grundlage fertigstellen (Pterodactyl Panel + node01, Automationen, Monitoring-Skelett).

## Key Workstreams
- Panel/Webserver Härtung, SSL, Backups (siehe [[04_Infrastruktur/Server Setup#Architektur-Überblick\|Server Setup#Architektur-Überblick]]).
- Node01 produktiv inkl. 2 Fokus-Games (z. B. Minecraft, Valheim) + Testbot-Server.
- **Data Platform MVP:** Docker Compose Setup (Postgres + Grafana) und ersten Ingest-Bot ("Observer") deployen.
- Proxmox Backup Client, Monitoring-Stack (Prometheus/Grafana) live, Alerts -> Ops Discord.
- Discord/Forum/Website MVP-Struktur (vgl. [[Plattformen & Community Touchpoints\|Plattformen & Community Touchpoints]]) fertig.

## Economic Focus
- Kostentracking pro Node (Hardware, Lizenz, Strom) + monatlicher Report.
- Angebotseinholung für node02/node03, Hosting-Rahmenvertrag abschließen.

## Check / KPIs
- Panel & node01 >99% Uptime in internen Tests.
- Backups (PBS + Panel) dokumentiert + Restore-Test bestanden.
- Data Platform empfängt erste Daten (Chat/Voice Logs) in Postgres.
- Discord + Forum + Website funktionsfähig, Grundregelwerke publiziert.

## Milestones & Owners
| Deliverable | Owner |
| --- | --- |
| Panel Hardening & SSL | Operations Director + Ops Engineer |
| node01 Live (2 Games + Bot Nest) | Ops Engineer |
| Data Platform MVP (DB + Bot) | Data Engineer |
| PBS Backup Script + Restore Test | Operations Director |
| Monitoring Stack (Prometheus, Grafana, Alerting) | Automation Squad |
| Discord/Forum/Website MVP (Rules, Structure) | Community Director + Growth Manager |

## Notes
- Document all runbooks im internen DevOps-Repo, Link in [[04_Infrastruktur/Server Setup\|Server Setup]].
- Output dient als Gateway für [[05_Phasenplan/Phase 2 Culture Pilot\|Phase 2 Culture Pilot]], ergo Lessons Learned sammeln.

↩ [[Home\|Home]] · Zurück zu [[05_Phasenplan/Phase 0 Strategic Reset\|Phase 0]] · Weiter zu [[05_Phasenplan/Phase 2 Culture Pilot\|Phase 2]]
