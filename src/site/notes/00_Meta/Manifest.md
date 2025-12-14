---
{"dg-publish":true,"permalink":"/00-meta/manifest/","dgPassFrontmatter":true,"noteIcon":"","created":"2025-12-13T16:00:35.664+01:00","updated":"2025-12-14T09:11:36.598+01:00"}
---

# Manifest – Herkunft, Haltung & Ambition

Das GG-N Manifest ist unser CEO-Briefing an die Zukunft: Es hält fest, woher wir kommen, was uns antreibt und wie wir skalieren, ohne unsere Wurzeln zu verlieren.

## Ursprung & Timeline
| Jahr | Meilenstein | Wirkung |
| --- | --- | --- |
| 2024 | Erste Random-Match-Frust-Session → Konzept [[00_Meta/Projektueberblick\|Projektueberblick]] | Fokus auf „mehr als Randoms“ entsteht. |
| 2025 | Governance Reset & Council-Aufbau ([[05_Phasenplan/Phase 1 Strategic Reset\|Phase 1 Strategic Reset]]) | Gleichberechtigte Dreierspitze definiert Rollenmodell. |
| 2026 | Launch & Growth-Loop ([[05_Phasenplan/Phase 5 Public Launch\|Phase 5 Public Launch]] → [[05_Phasenplan/Phase 7 Growth Sprint\|Phase 7 Growth Sprint]]) | Community proof of concept, Datenkultur verankert. |
| 2027+ | Monetization + Impact ([[05_Phasenplan/Phase 8 Monetization\|Phase 8 Monetization]] → [[05_Phasenplan/Phase 10 Sustainability\|Phase 10 Sustainability]]) | Finanzielle Nachhaltigkeit + ESG-Story. |

## North-Star Ambition
1. **100 % Vertrauenswürdige Community** – Kein Tag ohne Moderation, klare Regeln sichtbar auf allen Plattformen ([[Regelwerke/GG-N-AGB (DE)\|AGB]], [[Regelwerke/Discord-Regelwerk\|Regelwerke/Discord-Regelwerk]]).
2. **Selbsttragende Finanzen** – [[02_Ziele/Finanzielle Ziele\|Finanzielle Ziele]] + [[05_Phasenplan/Phase 8 Monetization\|Phase 8 Monetization]] sichern >100 % Cost Coverage + Reinvest-Puffer.
3. **Data-Driven Decisions** – Jeder große Schritt basiert auf einem KPI-Snapshot aus [[04_Infrastruktur/Data Platform\|04_Infrastruktur/Data Platform]] und landet im Council-Deck.
4. **Creator-positive Scaling** – Partnerschaften & Playbooks (z. B. [[05_Phasenplan/Taschengeld Funnel\|05_Phasenplan/Taschengeld Funnel]]) stärken junge Talente statt sie auszunutzen.

## Leitprinzipien
- **Vision Locked** – Jede Initiative referenziert [[01_Vision/Vision 2026\|Vision 2026]] & [[01_Vision/Zielgruppe\|Zielgruppe]]; Abweichungen müssen im Council begründet werden.
- **Transparente Ownership** – Rollen, Deputies, KPIs liegen offen in [[03_Rollen/Rollenuebersicht\|Rollenuebersicht]] & [[03_Rollen/Projektleitungen\|Projektleitungen]].
- **Psychologische Sicherheit** – Moderation/Support handeln nach [[03_Rollen/Moderation und Support Roles\|Moderation und Support Roles]], Feedback wird institutionalisiert.
- **Operational Excellence** – Runbooks + Server-Änderungen werden im [[Templates/Server-Change-Template\|Templates/Server-Change-Template]] dokumentiert; keine Schatten-Deployments.
- **Learning Publicly** – Erfolg & Scheitern wandern gleichermaßen in [[Templates/Meeting-Template\|Weekly Notes]].

## Strategische Säulen
1. **Community Core** – Discord/Forum/Events orchestriert über [[04_Infrastruktur/Plattformen\|Plattformen]], [[02_Ziele/Community Ziele\|Community Ziele]] & [[Templates/Event-Template\|Templates/Event-Template]].
2. **Growth & Monetization** – Omni-Channel-Kampagnen + Partnerdeck aus [[05_Phasenplan/Phase 7 Growth Sprint\|Phase 7 Growth Sprint]] & [[05_Phasenplan/Phase 8 Monetization\|Phase 8 Monetization]].
3. **Ops & Infrastructure** – Pterodactyl, Nodes, Automations nach [[04_Infrastruktur/Server Setup\|Server Setup]] + [[04_Infrastruktur/Data Platform\|04_Infrastruktur/Data Platform]].
4. **Compliance & Trust** – Risiko-Backlog + Gegenmaßnahmen aus [[06_Risiken/Risiken und Gegenmassnahmen\|Risiken und Gegenmassnahmen]], Privacy-Einhaltung, transparente VIP-Programme.
5. **Innovation Pods** – Dedizierte Slots für neue Playbooks (Taschengeld Funnel, Creator Labs) – dokumentiert im Abschnitt „Growth Playbooks“.

## Game & Server Portfolio Doctrine
- **Manifest Games** – Wir launchen nur Titel, die Community-Sicherheit, Modding-Kultur & Datenzugriff zulassen; Auswahl folgt [[01_Vision/Zielgruppe\|Zielgruppe]] + [[01_Vision/Vision 2026\|Vision 2026]].
- **Portfolio Rhythm** – Pro Phase maximal drei aktive „Games“, jedes mit Manifest Card (Hypothese, KPI, Owner, Exit-Kriterien) im [[Templates/Server-Change-Template\|Templates/Server-Change-Template]].
- **Scaling Ceiling** – 10–20 Server sind eingeplant; Infrastruktur wird pro Game als Stack dupliziert, nicht improvisiert (IaC + Observability first).

| Track | Game Fokus | Warum er Manifest-fit ist | Status |
| --- | --- | --- | --- |
| Sanctuary Sandbox | Minecraft (Paper/Purpur) | Sozialer Safe Space, Creator-freundlich, tiefe Mod-Integrationen. | Go (Phase 2) |
| Expedition Pods | Valheim / Core Survival | Squad-Coop stärkt Verbindlichkeit & Lernkurven. | Go (Phase 2) |
| Arena Scrims | CS2 / Aimlabs Rotation | Zeigt Kompetitivität + Fair-Play-Moderation. | Pilot später Phase 3 |
| Spotlight Slots | Rotierende Indie/Partner Games | Testbett für neue Communities & Sponsoren. | Backlog (Council-Approval) |

> Jede Erweiterung nutzt Playtests + Scorecard: Player Fit, technische Stabilität, monetäre Perspektive, Moderationsaufwand, Data-Zugriff.

### Server-Archetypen (V1)
| Archetyp | Purpose | Tooling & Guardrails | Owner |
| --- | --- | --- | --- |
| **Control Tower** | Pterodactyl Panel + GitOps Layer | Terraform Modules, GitHub Actions, Grafana/Prometheus, Secrets im Vault. | Ops Lead |
| **Sandbox Pods** | Minecraft Cluster (Lobby + Instanzen) | Paper + Proxy, gamedig Exporter, Anti-Grief Plugins, Data Pipeline [[04_Infrastruktur/Data Platform#B. Minecraft / Andere\|04_Infrastruktur/Data Platform#B. Minecraft / Andere]]. | Forward Deployed Infra |
| **Survival Pods** | Valheim/BepInEx Nodes | Automatic Backups, Config Drift Reports, SLA Board in [[03_Rollen/Projektleitungen\|03_Rollen/Projektleitungen]]. | Mission Squad Lead |
| **Competitive Pods** | CS2/Custom Dedicated Server | Tickrate Monitoring, Anti-Cheat Hooks, Match Logs in `_raw_competitive`. | Arena Captain |
| **Experiment Slots** | Kurzlebige Partner-/Indie-Server | Feature Flags, Budget Cap, Sunset-Checklist (Lessons → [[03_Rollen/Lessons Hub\|03_Rollen/Lessons Hub]]). | Growth Pod |

### Palantir-Style Ops DNA
- **Platform Core vs. Forward Deployed Pods** – Kleines Kernteam baut Templates + Tooling, Mission Pods passen sie pro Game/Squad an und reporten wöchentlich ins Council.
- **Zero-Shadow Deploys** – Kein Server ohne IaC Merge + Runbook. Änderungen werden via [[Templates/Server-Change-Template\|Templates/Server-Change-Template]] kommuniziert, Audit-Logs landen im [[04_Infrastruktur/Data Platform\|04_Infrastruktur/Data Platform]].
- **SLO Ownership** – Jeder Archetyp hat Response-Targets (Uptime, Ticket-SLA, Player Experience) und dedizierte Deputies (siehe [[03_Rollen/Rollenuebersicht\|03_Rollen/Rollenuebersicht]]).
- **Observability Default** – Logging/metrics/alerting aktiv vor Go-Live, inkl. Discord Status Alerts und Incident Trainig nach [[04_Infrastruktur/Incident Playbook\|04_Infrastruktur/Incident Playbook]].

## Lessons & Legacy Log
| Quartal | Insight | Impact |
| --- | --- | --- |
| Q1 2025 | Discord-Warteliste treibt bessere Member-Qualität als offene Invites. | Warteliste bleibt Standard (Phase 3 Pilot). |
| Q2 2025 | Ticket-Automation reduzierte SLA von 24h auf 6h. | Invest in Support SOPs priorisiert. |
| Q3 2025 | Early Beta Events steigern Retention; Solo-Events floppten. | Nur Squad-Events in Phase 4 Rollouts. |
| Q4 2025 | Ops-Team-Shadowing senkte Onboarding-Zeit für Mods um 30 %. | Pflichtprogramm für neue Welcome Guides. |

> Jede Phase finalisiert Lessons Learned im Meeting-Template; relevante Erkenntnisse landen hier.

## Future Bets
| Initiative | These | Phase Slot | Next Step |
| --- | --- | --- | --- |
| Creator Labs | Kuratierte Creator-Booster bringen Sponsoring + Community Reach. | [[05_Phasenplan/Phase 7 Growth Sprint\|Phase 7 Growth Sprint]] | Playbook schreiben (siehe [[05_Phasenplan/Playbook Backlog\|05_Phasenplan/Playbook Backlog]]) |
| Education Hub | Lernquests + Eltern-Workshops → Trust + neue Revenue Streams. | [[05_Phasenplan/Phase 10 Sustainability\|Phase 10 Sustainability]] | Pilot-Kit für Eltern entwickeln. |
| Esports Academy | Coaching & Ladder stärken Retention + Paid Offerings. | [[05_Phasenplan/Phase 9 Expansion\|Phase 9 Expansion]] | Partner-Scouting + Curriculum draft. |
| IRL Pop-ups | Offline Meetups stärken Loyalität & PR. | [[05_Phasenplan/Phase 6 Stabilize Automate\|Phase 6 Stabilize Automate]] | Budgetschätzung + Location Check. |
| Media Network | Eigene Content-Serie als Awareness Engine. | [[05_Phasenplan/Phase 8 Monetization\|Phase 8 Monetization]] | Media Kit 3.0 planen. |

## 10-Phasen-Cadence
- **Phasen 1–3** = Fundament (Governance, Infra, Kultur). Fokus: Struktur, Tooling, Werte.
- **Phasen 4–6** = Öffnung & Automatisierung. Fokus: Launch, Community Proof, SOPs.
- **Phasen 7–9** = Wachstum & Expansion. Fokus: Experimente, Monetarisierung, internationale Satelliten.
- **Phase 10** = Nachhaltigkeit. Fokus: ESG, Nachfolge, Impact Reporting.
- Nach Phase 10 beginnt der Zyklus bewusst neu – mit Lessons Learned zurück zu [[05_Phasenplan/Phase 1 Strategic Reset\|Phase 1 Strategic Reset]].

## Operating Rhythm (CEO-Perspektive)
- **Weekly Council** – Status aller Phasen + Risiko-Review, Dokumentation im Meeting-Template.
- **Monthly Manifest Check-In** – Passt unser Handeln noch zu Prinzipien & Timeline? Falls nein → Manifest ergänzen.
- **Quarterly State of the Guild** – Öffentliche Townhall + Update im Digital Garden (nutzt [[04_Infrastruktur/Digital Garden Publishing\|04_Infrastruktur/Digital Garden Publishing]]).
- **Annual Reset** – Phase-10-Review, Budget-Neuaufstellung, Offsite zur Kurskorrektur.

## Skalierungsleitplanken
- **Heritage sichtbar halten** – Home, Manifest und Timeline bleiben fix. Screenshots & Milestones gehören ins Vault, nicht nur in Social Posts.
- **Experimente mit Guardrails** – Jedes Playbook erhält Owner, Hypothese, KPI & Risk Link (z. B. [[05_Phasenplan/Taschengeld Funnel\|05_Phasenplan/Taschengeld Funnel]] ↔ [[06_Risiken/Risiken und Gegenmassnahmen\|Risiken und Gegenmassnahmen]]).
- **Feedback-Schleifen** – Nach jeder Phase Retro im Meeting-Template + Backlog/TODO Update ([[07_Naechste_Schritte/Shortlist\|Shortlist]]).
- **Responsible Growth** – Compliance, Eltern-/Partner-Kommunikation und Data Privacy sind nicht verhandelbar; referenziere regelmäßig [[Regelwerke/Privacy-Notice\|Regelwerke/Privacy-Notice]].

## Next CEO Actions
- [ ] Timeline erweitern (Quarterly Highlights mit Zahlen).
- [ ] `dg-pinned` setzen, sobald Garden-Navigation final ist.
- [ ] Manifest in Onboarding verankern (verlinkt in [[03_Rollen/Erste Besetzung\|Erste Besetzung]] & Rollenbriefings).
- [ ] Dedizierte „Lessons Learned“ Sektion ergänzen, sobald Phase-2 Retro abgeschlossen ist.

↩ [[Home\|Home]]

↩ [[Home\|Home]]
