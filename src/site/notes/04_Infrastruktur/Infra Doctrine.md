---
{"dg-publish":true,"permalink":"/04-infrastruktur/infra-doctrine/","dgPassFrontmatter":true,"noteIcon":"","created":"2025-12-14T09:14:49.211+01:00","updated":"2025-12-14T09:14:49.212+01:00"}
---

# Infra Doctrine – Autonomie, Scale & Ops Exzellenz

> Ergänzt das [[00_Meta/Manifest\|00_Meta/Manifest]] und macht klar, wie wir Infrastruktur betreiben, ohne von Fremdplattformen abhängig zu sein. Owner: Ops Captain · Deputies: Server Pilot, Data Platform Lead.

## 1. Zweck & Scope
- **Autonomie:** Core-Services (Panel, Game Nodes, Bots, Datenplattform) laufen auf von uns kontrollierten Maschinen (Colo/Dedicated). SaaS nutzen wir nur für Austauschbare (Status Page, Alerts).
- **Scale by Design:** Alles wird so dokumentiert, dass wir 1 → 20 Server über denselben Blueprint ausrollen können (IaC + Observability + Runbooks).
- **Community Impact:** Jede Infra-Entscheidung dient Member Experience, Creator-Schutz und Vertrauen (siehe [[01_Vision/Vision 2026\|Vision 2026]], [[Regelwerke/Privacy-Notice\|Regelwerke/Privacy-Notice]]).

## 2. Leitprinzipien
1. **Code before Clicks** – Infrastrukturänderungen kommen aus Repos (Terraform/Ansible) → [[Templates/Server-Change-Template\|Templates/Server-Change-Template]] → Deploy.
2. **Vendor Agnostic** – Keine Abhängigkeit von proprietären Panels/Cloud-Features, die sich nicht self-hosten lassen. Datenexporte sind Pflicht.
3. **Defense in Depth** – Netzsegmente, Secrets, Monitoring, Backups. Kein alleinstehender Server ohne Observability (siehe [[04_Infrastruktur/Server Setup\|04_Infrastruktur/Server Setup]] & [[04_Infrastruktur/Incident Playbook\|04_Infrastruktur/Incident Playbook]]).
4. **Forward Deployed Pods** – Plattformkern liefert Templates; Mission Pods passen sie an Games an und dokumentieren Lessons im [[03_Rollen/Lessons Hub\|03_Rollen/Lessons Hub]].
5. **Operational Transparency** – Auslastung, Kosten, Incidents werden monatlich im Council geteilt (verlinkt nach [[07_Naechste_Schritte/State of the Guild Deck\|07_Naechste_Schritte/State of the Guild Deck]]).

## 3. Layered Architecture
| Layer | Inhalt | Tools / Standards |
| --- | --- | --- |
| **Physical / Host** | Dedicated Roots / Colo Nodes (node01+), Management Network, IP + DNS | Debian 13 LTS, Tailscale/WireGuard, `nodeXX.gg-n.de` Namensschema |
| **Control Plane** | Pterodactyl Panel, GitOps Repo, Secrets Vault | Pterodactyl, Terraform Modules, SOPS + age, GitHub Actions CI |
| **Workload Pods** | Game Servers, Discord Bots, Web Services | Docker, Game-specific Eggs, `bot-*` Profiles |
| **Data & Observability** | Metrics, Logs, Dashboards, Data Platform | Prometheus, Loki, Grafana, [[04_Infrastruktur/Data Platform\|04_Infrastruktur/Data Platform]] |
| **Access & Governance** | RBAC, Secrets, On-Call, Audits | 1Password/Bitwarden Vault, SSH CA, [[03_Rollen/Projektleitungen\|03_Rollen/Projektleitungen]], [[04_Infrastruktur/Incident Playbook\|04_Infrastruktur/Incident Playbook]] |

## 4. Unabhängigkeits-Playbook
- **Hardware Mix:** 70 % Dedizierte Server/Colo (Leistung + Datenhoheit), 30 % Cloud Burst (Events). Für jedes Cloud-Asset muss ein „Bring-Home“-Pfad dokumentiert sein.
- **Mirrors & Escape Hatches:** Automatische Backups (PBS/S3), Config Dumps, Export-Skripte für Bots und Metrics, damit ein Provider-Wechsel < 7 Tage möglich ist.
- **License Hygiene:** Nur Open-Source oder kaufbare One-Time Licenses. Bei SaaS (z. B. BetterStack) wird Self-Hosted Alternative benannt (Uptime Kuma) und funktionsfähig gehalten.
- **Network Sovereignty:** Eigene DNS bei demselben Registrar, IPv4/6 Adressen dokumentiert. Notfall-Liste mit Support-Kontakten der Provider.
- **Dependency Register:** Tabelle im Ops Repo: Dienst → Owner → Hosting → Exit-Plan. Monatscheck im [[00_Meta/Manifest#Operating Rhythm (CEO-Perspektive)\|00_Meta/Manifest#Operating Rhythm (CEO-Perspektive)]].

## 5. Skalierungsmodell (10–20 Server)
1. **Capacity Model:** Spreadsheet + Grafana-Dashboard `GGN-Capacity` zeigen CPU/RAM-Auslastung, „Time to 80 %“. Ab 65 % Auslastung → Pre-order nächster Node.
2. **Node Archetypes:** Control Tower, Sandbox, Survival, Competitive, Experiment (siehe [[00_Meta/Manifest#Server-Archetypen (V1)\|00_Meta/Manifest#Server-Archetypen (V1)]]). Neue Server müssen einem Archetyp entsprechen oder einen neuen per Council ADR definieren.
3. **Deployment Packs:** Jede Node-Klasse hat ein Pack (Terraform Vars, Ansible Playbook, Monitoring Dashboards, Runbook). Packs liegen im Git Repo `infra/manifests`.
4. **Rollout Ritual:**
   - Draft Change → Review (Ops Captain + Mission Lead)
   - Staging Deploy (wenn vorhanden)
   - Production Deploy
   - Post-Deploy Check (Monitoring green, Security scan)
   - Documentation Update (`Notes/node0X.md`, [[Templates/Server-Change-Template\|Templates/Server-Change-Template]])
5. **Lifecycle:** Commission → Active → Warm Standby → Sunset. Sunset bedeutet: Backups archivieren, DNS entfernen, Costs/Tickets schließen, Lessons in [[03_Rollen/Lessons Hub\|03_Rollen/Lessons Hub]].

## 6. Automation Stack
- **Terraform Modules:** DNS, Proxmox/LXC, Pterodactyl Nodes, Prometheus Stack. Module katalogisiert in `infra/terraform/README`.
- **Ansible Playbooks:** OS Hardening, Docker Setup, Bot Deployment, Backup Agents. Playbooks signiert; CI lint per `ansible-lint`.
- **GitHub Actions Pipelines:**
  - `plan` Job auf PR → Terraform Plan, Ansible Dry Run.
  - `deploy` Job nur via Manual Approval (Ops Captain).
  - Secrets via OIDC + Vault token exchange.
- **Config Drift Checks:** Nightly job ruft `terraform plan` + `ansible --check` gegen alle Nodes, posted Delta in `#ops-alerts`.
- **Inventory Source of Truth:** `inventory.yaml` + `hosts.csv` (synced). Wird von Runbooks, Monitoring, On-Call benutzt.

## 7. Observability & Ops
- **Golden Signals:** Latency, Traffic, Errors, Saturation für Panel, API, Game Ports.
- **Tracing & Logs:** Loki Stack sammelt Panel Logs, Game Server stdout/stderr, Bot Logs. Retention 14 Tage, Critical 90 Tage.
- **Alerting Policy:** Severity 1 = Incident Bridge + Council, Severity 2 = Ops Channel + Status Update, Severity 3 = Async Backlog. Siehe [[04_Infrastruktur/Incident Playbook\|04_Infrastruktur/Incident Playbook]].
- **SLOs:** 
  - Panel Uptime 99.3 % / Monat.
  - Game Nodes 99 % / Node, 0 Major incidents ohne Postmortem.
  - Ticket Bots Response < 5 Min. 
  SLO-Reviews laufen im Monthly Manifest Check-In.
- **Runbooks:** Jede Service-Gruppe pflegt Troubleshooting Steps (DNS, Wings, Game-specific). Runbooks liegen neben Service Repo und verlinken ins Meeting Template.

## 8. Security & Access
- **Identity:** SSH Keys via `ssh-ca gg-n` + short-lived certs. Panel logins SSO (Keycloak) oder TOTP.
- **Secrets:** SOPS + age Files, stored encrypted in Git. Rotationsplan quartalsweise (siehe Risk Register).
- **Network:** Default Deny Firewall, Ports per Service. Private mgmt network via Tailscale. Game Ports offen via `ufw allow <port>`.
- **Audits:** Halbjährliche Security Review (Logs, Access, Backups). Findings → [[06_Risiken/Risiken und Gegenmassnahmen\|Risiken und Gegenmassnahmen]].
- **Compliance Prep:** DSGVO/Privacy Mapping – wo liegen Daten, wer hat Zugriff, Retention. Data Processing Agreements archiviert in `Legal/`.

## 9. Execution Roadmap (2025)
| Quartal | Fokus | Deliverables |
| --- | --- | --- |
| **Q1 (Phase 2)** | Core Blueprint | Terraform + Ansible Repo live, Node01 voll dokumentiert, Capacity Dashboard, Change Template Pflicht. |
| **Q2 (Phase 3)** | Multi-Node Ops | Node02 live, IaC tested via Game Day, Vault rollout, Config Drift Alerts aktiv. |
| **Q3 (Phase 4/5)** | Observability & Bots | Loki Stack, Status Page, Bot Fleet CI/CD, Data Platform Bronze→Silver Automations. |
| **Q4 (Phase 6)** | Resilience | Warm Standby Node, Backup Restore Drills, Chaos Test, Playbook Update für Expansion. |

## 10. ToDos & Ownership
- [ ] `infra/terraform` Repo initialisieren + Module für Panel + Nodes (Owner: Ops Captain, Due: Feb 10).
- [ ] Inventory Template (`inventory.yaml`) anlegen und in [[04_Infrastruktur/Server Setup\|04_Infrastruktur/Server Setup]] verlinken (Owner: Server Pilot).
- [ ] Config Drift Workflow (GH Actions) einrichten (Owner: Tech Lead Deputy).
- [ ] Exit-Pläne für alle SaaS (BetterStack, Ticket Tool) dokumentieren (Owner: Ops Captain + Player Support Lead).
- [ ] Monthly Ops Report Template → [[Templates/Meeting-Template\|Templates/Meeting-Template]] integrieren (Owner: Data Platform Lead).

↩ [[04_Infrastruktur/Server Setup\|04_Infrastruktur/Server Setup]] · [[00_Meta/Manifest\|00_Meta/Manifest]] · [[04_Infrastruktur/Data Platform\|04_Infrastruktur/Data Platform]] · [[04_Infrastruktur/Incident Playbook\|04_Infrastruktur/Incident Playbook]]
