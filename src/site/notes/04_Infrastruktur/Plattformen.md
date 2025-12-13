---
{"dg-publish":true,"permalink":"/04-infrastruktur/plattformen/","dgPassFrontmatter":true,"noteIcon":"","created":"2025-12-08T16:42:13.606+01:00","updated":"2025-12-13T14:41:39.197+01:00"}
---

# Plattformen & Community Touchpoints

Ausbaustufen für Discord, Forum, Website und Social Media. Ziel: direkte Einzahl auf [[02_Ziele/Community Ziele\|Community Ziele]] (aktive Member, Events/Teilnahme, Chat-Aktivität).

## Discord Hub
- **Ziele:** 100 % der aktiven Member im Server, „kein toter Tag“ Indicator.
- **Struktur:** Kategorien Info / Community / Games / Support / Staff (vgl. [[05_Phasenplan/Phase 1 Infrastructure Build\|Phase 1 Infrastructure Build]]).
- **Tasks:**
  - [ ] Automations (Welcome, Role Selection, Ticket Bot) produktiv nehmen.
  - [ ] Events-Tab pflegen (alle Termine mit „Interested“ Tracking → KPI).
  - [ ] Community Pulse Channel (Feedback, Surveys) → Input für [[02_Ziele/Community Ziele\|Community Ziele]].
  - [ ] Permissions strikt nach [[03_Rollen/Community Hierarchy\|Community Hierarchy]].
- **Bots & Automations:** `Ticket Tool` (Support), `Statbot` (Message & Voice Analytics), `Sesh` (Events), eigener „Bridge Bot“ für Website-Formulare → Discord Threads.
- **KPIs & Reporting:** Weekly Active Users (über Statbot API), Event RSVPs (Sesh export), Support Ticket SLA (Ticket Tool Webhook in Sheets) → Report im Meeting-Template.

## Forum & Knowledge Base
- **Ziele:** 30 % der Member nutzen Forum/Threads für Bewerbungen & Support (Entlastung Discord).
- **Module:** Bewerbungsbereich, Guides/Wikis, Dev-Blog, Staff-Log.
- **Tasks:**
  - [ ] Regelwerk + AGB/Privacy (siehe [[Regelwerke/Forum-Regelwerk\|Regelwerke/Forum-Regelwerk]], [[Regelwerke/GG-N-AGB (DE)\|Regelwerke/GG-N-AGB (DE)]], [[Regelwerke/Privacy-Notice\|Regelwerke/Privacy-Notice]]) integrieren.
  - [ ] Formulare/Templates pinnen (Bewerbungen, Reports, Feedback).
  - [ ] Single Sign-On (Discord OAuth) evaluieren, damit Onboarding smooth läuft.
- **Verlinkung:** Von Discord Announcements & Website CTA direkt aufs Forum lenken.
- **KPI Tracking:** Foren-Software (z. B. Discourse/Invision) liefert API → Dashboard: Neue Themen/Tag, aktive Member, beantwortete Tickets. Export via Zapier/Integromat zu Google Sheets → Abgleich mit [[02_Ziele/Community Ziele\|Community Ziele]].

## Website / Landingpage
- **Ziele:** Conversion Funnel → 40 % der Besucher klicken „Join Discord“, 10 % tragen sich für Newsletter/Events ein.
- **Sektionen:** Who we are, Games, Events, Rules Light, Join Us, Partner.
- **Tasks:**
  - [ ] CTA Buttons tracken (Plausible/GA4).
  - [ ] Event-Highlights & KPIs aus [[02_Ziele/Community Ziele\|Community Ziele]] als Social Proof einbauen.
  - [ ] Embed Forum/Discord Widgets (Regelwerk, aktuelle Events) für Trust.
  - [ ] SEO-Basics: Meta Tags, OG-Images (aus [[04_Infrastruktur/Domains und Branding\|Domains und Branding]]).
- **Forms & Ticket-Integration:**
  - Bewerbungsformular → Sends POST → Cloud Function → erzeugt Discord Ticket (Ticket Tool API) + Eintrag im Forum.
  - Newsletter-Signups → ConvertKit/Mailcoach, Auto-Tag „Prospect“, an Growth Director Report.
  - VIP/Supporter Form → webhook → Merch & VIP Manager + CRM Sheet.

## Social Media & Content Loop
- **Primärkanäle:** Instagram/TikTok (Clips), optional X/Twitter für News, YouTube Shorts für Recaps.
- **Ziele:** Jede Woche 1–2 Clips aus Events (→ KPI „Mind. 1 Event/Woche“).
- **Tasks:**
  - [ ] Content Calendar (Figma/Notion) – Format: Highlights, Member Spotlight, Behind the Scenes.
  - [ ] UGC Guidelines: Member können Clips einreichen → Growth Manager kuratiert.
  - [ ] Cross-Promo mit Creator Alliance (siehe [[03_Rollen/Community Hierarchy#Partner & Supporter Groups\|Community Hierarchy#Partner & Supporter Groups]]).
  - [ ] Track KPIs (Views, CTR auf Discord/Website) und in [[02_Ziele/Community Ziele\|Community Ziele]] spiegeln.
- **Automation:** Zapier/Integromat Workflows → Social Stats -> Data Warehouse (Google Sheets/Notion DB). Wöchentlicher Export in Meeting-Note.

## Integrationen & Tooling
- [ ] Discord → Forum Thread Bridge (z. B. via Discord Forum Channels oder Webhooks).
- [ ] Website → Social Auto-Embed (Latest posts, event recaps).
- [ ] Newsletter/Automation (Mailcoach/ConvertKit) für VIP/Sponsor News.
- **KPI Dashboard:** Prometheus/Grafana für Infra, Google Data Studio/Looker für Community KPIs (Discord WAU, Forum Posts, Website CTR, Game Server Player Count). Weekly Snapshot an [[02_Ziele/Community Ziele\|Community Ziele]] anhängen.

↩ [[Home\|Home]] · Ergänzend: [[04_Infrastruktur/Domains und Branding\|Domains und Branding]], [[04_Infrastruktur/Server Setup\|Server Setup]], [[02_Ziele/Community Ziele\|Community Ziele]]
