---
{"dg-publish":true,"permalink":"/04-infrastruktur/server-setup/","dgPassFrontmatter":true,"noteIcon":"","created":"2025-12-08T16:42:15.934+01:00","updated":"2025-12-13T14:41:39.197+01:00"}
---

# Server-Setup & Bots

> Alle Deployments und Änderungen unbedingt im [[Templates/Server-Change-Template\|Server-Change-Template]] dokumentieren.

## Architektur-Überblick
- **Panel (Webserver):** Pterodactyl Panel läuft bereits auf dem bestehenden Webserver (Debian 13). Wartung & Updates erfolgen nach Release Notes von Pterodactyl (Panel + Daemon getrennt planen).
- **Wings Nodes:** Dedizierte Gameserver (node01, später node02, node03 …) hosten die eigentlichen Instanzen. Jeder Node nutzt Debian 13 + Docker.
- **Backbone:** Tailscale/ WireGuard (optional) oder direkte Firewall-Regeln (Ports 22/2022, 8080, Game-Ports). Monitoring via UptimeRobot/Prometheus.
- **Bots & Automation:** Discord-/TS-Bots laufen getrennt auf kleinen VMs oder im Panel als „bot-servers“.

## Node01 – Dedicated Game Server
**Zweck:** Primärer Host für Fokus-Games + Testserver.

- **Hardware / OS:** Dedicated Machine, Debian 13, Docker Engine + docker-compose installiert.
- **Vorbereitung:**
  - [ ] DNS-Einträge für `node01.gg-n.de` → dedizierte IP.
  - [ ] Firewall-Regeln (Allow: 22/tcp, 8080/tcp, Game-Ports, ggf. 443 für Web-Interfaces).
  - [ ] System-Updates: `apt update && apt upgrade -y`, Kernel prüfen.
- **Pterodactyl Wings Setup:**
  1. Panel → Admin → Locations → `LOC-DE-01`.
  2. Node hinzufügen: Name `node01`, FQDN `node01.gg-n.de`, HTTP/HTTPS Ports setzen, Daemon-Secret kopieren.
  3. Auf node01:
  ```bash
     curl -sSL https://get.docker.com/ | bash
     apt install -y curl tar unzip
     ```
     Wings installieren:
     ```bash
     cd /etc/pterodactyl
     curl -Lo wings.tar.gz https://github.com/pterodactyl/wings/releases/latest/download/wings_linux_amd64
     ```
     Config aus dem Panel speichern (`/etc/pterodactyl/config.yml`), Service anlegen:
     ```bash
     useradd -r -m -d /var/lib/pterodactyl -s /bin/false pterodactyl
     chown -R pterodactyl:pterodactyl /etc/pterodactyl /var/lib/pterodactyl
     systemctl enable --now wings
     ```
  4. Verbindung prüfen: Panel → Nodes → `node01` → Status = Grün.
- **Game Deployment Workflow:**
  - [ ] Create Egg & Service im Panel (Minecraft, Valheim, etc.).
  - [ ] Assign Allocation Ports (z. B. 25565, 25575 …).
  - [ ] Deploy Server → Test (Ping, Join, RCON).
  - [ ] Monitoring & Alerts aufsetzen (Prometheus Node Exporter, Discord Webhooks).

## Weitere Nodes hinzufügen (node02, node03 …)
> Ziel: horizontale Skalierung bereit halten, sobald neue Games oder Load benötigt werden.

1. **Hardware bereitstellen:** Dedizierter Server oder vServer mit Debian 13.
2. **Netzwerk/ DNS:**
   - Subdomain `node0X.gg-n.de`, Reverse DNS anpassen.
   - Firewall-Template von node01 übernehmen (nur benötigte Ports öffnen).
3. **Panel-Konfiguration:**
   - Neue Location falls anderes Rechenzentrum, sonst `LOC-DE-01`.
   - Node-Name, Memory/Disk Limits definieren, Upload/Download-Limits setzen.
4. **Wings-Installation:** Gleich wie node01 (Script + config.yml). Service starten und Panel-Status kontrollieren.
5. **Tagging:** Nodes im Panel taggen (z. B. `prod`, `test`, `event`) → hilft Scheduling.
6. **Capacity Planning:**
   - Sheet pflegen: RAM, CPU, Storage, belegte Slots.
   - Alert, wenn Auslastung > 75 % → nächste Node vorbereiten.
7. **Dokumentation:** Für jeden Node eigenständige Notiz im Obsidian oder Pterodactyl Panel (z. B. `Notes/node02.md`) mit Hardware, Wartungsfenster, Ansprechpartner.

## Wartung & Backups
- **Backups (Proxmox Backup Client):** Alle Nodes werden mittels `proxmox-backup-client` gesichert. Beispielskript (`/usr/local/bin/ggn-backup.sh`):
  ```bash
  #!/bin/bash
  export PBS_PASSWORD='{{env:PBS_PASS}}'
  TIMESTAMP=$(date +%F-%H%M)
  proxmox-backup-client backup \
    etc.pxar:/etc \
    pterodactyl.pxar:/var/lib/pterodactyl \
    docker-volumes.pxar:/var/lib/docker/volumes \
    --repository pbs@ssl://backup.gg-n.de:8007/pbs1 \
    --backup-id node01 \
    --backup-time "$TIMESTAMP" \
    --encrypt backupkey.pxar \
    --notes "node01 nightly"
  ```
  - Cronjob: `0 3 * * * root /usr/local/bin/ggn-backup.sh >> /var/log/ggn-backup.log 2>&1`
  - Restores monatlich testen (`proxmox-backup-client mount ...` → Test-Restore).
  - Backups werden zusätzlich über S3/Wasabi mit Panel-internen per-Server Snapshots kombiniert (kritische Gameserver: nightly; generische: 3x/Woche).
- **Updates:** Quartalsweise Panel/Wings Updates (Staging Node zuerst). Changelog dokumentieren.
- **Monitoring:** Node Exporter + Prometheus/Grafana oder einfache UptimeRobot Checks. Alerts ins Ops Discord Channel.
- **Security:** SSH nur via Keys, Fail2ban aktivieren, automatisierte Security-Updates (unattended-upgrades).

### Server Monitoring Stack
- **Prometheus Node Exporter** auf jedem Node (Port 9100), optional Pterodactyl Stats Exporter.
- **Prometheus Server** (kann auf Webserver oder dedizierter VM laufen) + Grafana Dashboard `GGN-Ops`.
- **Alertmanager:** Alerts → Discord Webhook `#ops-alerts` (CPU > 85 %, RAM > 90 %, Wings down, Docker service down).
- **Game-specific Monitoring:** use gamedig exporter for Minecraft/Valheim to check player count.
- **External Uptime (Layer 7):** UptimeRobot or BetterStack hitting `panel.gg-n.de`, `api.gg-n.de`, each Gameserver port to catch firewall issues.

## Bot-Infra
- **Discord Moderation Bot:** Läuft als Service im Panel (separater Nest) oder auf Webserver. Document tokens/secrets im Vault (nicht in Repo). Empfehlung: `Moderator.GG` (Eigenentwicklung) oder etablierte Bots (z. B. `Dyno` für Automod).
- **Ticket Bot:** `Ticket Tool` (self-hosted Premium Version) oder `Helper.gg`. Vorteil: Web-Dashboard + Discord UI, API-Webhook zu Website Formularen. Self-host-Container auf node01 (`ticket-bot` Nest).
- **Website ↔ Discord Tickets:** Landingpage-Formular sendet POST → Cloud Function (e.g. Cloudflare Worker) → Ticket Tool API → erstellt Ticket + sendet Bestätigungsmail.
- **Logging & Analytics Bot:** `Statbot` oder `Apollo` (für Events). Alternativ eigener Bot, der Discord Metrics → InfluxDB/Grafana schreibt (Weekly WAU & Message Count = KPI feed).
- **Role Management Reactions:** `Carl-bot`/`Sesh` für Events, Reaction Roles, Auto-Moderator.
- **TS3 Bot (SinusBot o. Ä.):** Auf node01 oder dedizierter VM, Ports + Firewall anpassen.

## To-Do & Tracking
- [ ] Fokus-Games definieren und als Eggs/Docker-Images vorbereiten.
- [ ] node01 vollständig auditieren (Checkliste oben).
- [ ] node02 Plan erstellen (Hardware-Angebote, Termin).
- [ ] Backup-Jobs testen (Restore-Test quartalsweise).
- [ ] Monitoring-Dashboards im Ops-Channel vorstellen.

Verzahnung mit [[05_Phasenplan/Phase 1 Infrastructure Build\|Phase 1 Infrastructure Build]] (Stabilität), [[05_Phasenplan/Phase 4 Public Launch\|Phase 4 Public Launch]] (Kapazität) und [[03_Rollen/Rollenuebersicht#Division: IT & Staff Operations\|IT & Staff Division]] sicherstellen.

↩ [[Home\|Home]]
