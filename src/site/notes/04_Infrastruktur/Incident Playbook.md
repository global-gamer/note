---
{"dg-publish":true,"permalink":"/04-infrastruktur/incident-playbook/","dgPassFrontmatter":true,"noteIcon":"","created":"2025-12-13T16:36:57.201+01:00","updated":"2025-12-13T16:36:57.201+01:00"}
---

# Incident & On-Call Playbook

Standard Operating Procedure für Ausfälle, Eskalationen und Postmortems. Owner: Operations Director, Deputies: Ops Engineer + Support Captain.

## Escalation Tree
1. **Tier 0 (Alert Trigger)** – Prometheus/Alertmanager, Bot Monitoring, Community Reports.
2. **Tier 1 (On-Call Engineer)** – Ops Engineer (Rotation). Reaktionszeit < 10 Min.
3. **Tier 2 (Director Escalation)** – Operations Director + Backup (Growth/Community Directors bei Impact auf Member).
4. **Tier 3 (Executive Council)** – Nur bei Datenverlust, Security, Reputationsrisiko.

Channel-Matrix:
- `#ops-alerts` (Discord) – Automatisches Alerting + laufender Thread.
- `#council-war-room` – Falls Major Incident, cross-division sync.
- Status Page (TODO) – Öffentliche Updates.

## Incident Workflow
1. **Detection** – Alert, User-Report oder Monitoring schlägt an.
2. **Triage** (On-Call):
   - Impact? (Users, Revenue, Reputation)
   - Scope? (Discord, Game Servers, Payments, Data)
   - Immediate mitigation? (Restart, reroute, communication)
3. **Communication**:
   - Update `#ops-alerts` Template:
     ```
     🛎 Incident Start
     - Time: 
     - Impact: 
     - Owner: 
     - Next update: 
     ```
   - Bei Public Impact: Discord Announcements + Status Page nach 15 Min.
4. **Mitigation** – Technische Maßnahmen, ggf. Rollback/Failover.
5. **Resolution** – Incident geschlossen, Summary ins Template.

## Postmortem Template
- **Summary**: Was ist passiert? Timeline + Impact.
- **Root Cause**: Technische / Prozessfehler.
- **Detection**: Wie wurde es erkannt? (Monitoring, User, Zufall)
- **Response**: Was lief gut? Was nicht?
- **Action Items**:
  - [ ] Fix 1 – Owner – Due Date
  - [ ] Fix 2 – Owner – Due Date
- **Communication Review**: Discord/Status Page/Partner Alerts.
- **Links**: Grafana Dashboards, Logs, PRs.

Alle Postmortems im Vault (Ordner `04_Infrastruktur/Postmortems`) ablegen und in [[Templates/Meeting-Template\|Templates/Meeting-Template]] verlinken.

## On-Call Rotation
- **Week 1**: Ops Engineer
- **Week 2**: Tech Lead Deputy
- **Week 3**: Operations Director (fallback)
- **Support Captain** übernimmt Kommunikation (Ticket Updates, Community Messaging).
- Kalender (Google/Obsidian) pflegen, On-Call Handover im Meeting ansprechen.

## Tooling & Automation
- Alertmanager → Discord Webhook `#ops-alerts`.
- PagerDuty/ntfy (Optional) für SMS/Push.
- Loki + Grafana Tempo für Logs/Traces (Phase 6).
- Incident Forms (Google/Garden) für Member Reports → Ticket Tool Integration.

## Training & Drills
- Quartalsweise „Game Day“ (Chaos Test) – Node Fail, Discord Bot Outage, Payment Error.
- Shadowing für Deputies (Senior Mod, Creator Manager) um cross-division Impact zu verstehen.
- Lessons Learned in [[03_Rollen/Lessons Hub\|Lessons Hub]] sammeln → Manifest aktualisieren.

↩ [[04_Infrastruktur/Server Setup\|Server Setup]] · [[Templates/Meeting-Template\|Templates/Meeting-Template]] · [[Home\|Home]]
