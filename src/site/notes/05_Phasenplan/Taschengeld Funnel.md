---
{"dg-publish":true,"permalink":"/05-phasenplan/taschengeld-funnel/","dgPassFrontmatter":true,"noteIcon":"","created":"2025-12-13T13:21:20.179+01:00","updated":"2025-12-13T16:04:36.980+01:00"}
---

# Taschengeld Funnel - Hypothese

Meta-Notiz zu einem aggressiveren, spielerischen Monetarisierungskonzept für jüngere Zielgruppen (8-16 Jahre). Gedankenspiel für [[05_Phasenplan/Phase 8 Monetization\|Phase 8 Monetization]] und die [[02_Ziele/Finanzielle Ziele\|Finanzielle Ziele]]. Ziel ist, den kompletten Journey von Erstkontakt bis Loyalitätsprogramm zu skizzieren.

## Zielgruppen-Segmente
- **Sprinter (8-10, Taschengeld wöchentlich)**: Kaufen impulsiv, reagieren stark auf glitzernde Cosmetics und begrenzte Angebote. Eltern müssen häufig bestätigen, daher Fokus auf Micro-Transactions.
- **Grinder (11-13, Schulhof-Coaches)**: Haben mehr Bildschirmzeit und Social Proof Value. Wollen in Leaderboards auffallen, akzeptieren Abo-Modelle wenn sie Vorteile im Squad liefern.
- **Streamerlings (14-16, Creator-affin)**: Sind in Discord/YouTube unterwegs, reagieren auf Creator-Codes, akzeptieren höhere Warenkörbe (15-25 €) wenn exklusive Statussymbole winken.

## Journey A-Z
| Stage | Trigger | Primary Taktiken | KPI |
| --- | --- | --- | --- |
| Awareness | Freund lädt ein, sieht Clip | Creator-Siegel, Micro ads mit "Pocket Battles Club" | CTR 5 % |
| Onboarding | Kostenlose Woche | Guided Quest, Sammelkarte mit grauen Rewards | 80 % completes tutorial |
| First Spend | Zwangsstopp nach Mission 3 | 0,99 € Starter Shine + Ein-Klick-Wallet | 45 % Conversion |
| Habit Loop | Daily FOMO Missions + Teamdruck | Quest Reset 24h, Bonus Slot | 60 % D1 retention |
| Deep Spend | Loot-Rotation an Wochenenden | Mystery-Packs, Limited Bundles | 30 % kaufen Add-ons |
| Advocacy | Creator-Referral oder Guild Lead | Team Buff + Sticker Drops | 20 % laden 2 Freunde ein |

## Feature Stack
### Pocket Battles Club 2.0
- Gratis-Season (7 Tage) mit sichtbar verriegelten Rewards. Nur das erste kosmetische Item wird freigeschaltet, alle weiteren zeigen Countdown + "Taschengeld-Top-up" Hinweis.
- Sammelkarte mit 20 Feldern; Felder 4, 8, 12, 16 sind "Premium Gates" die ohne Zahlung nicht aufklaren.

### Taschengeld Wallet
- Einmalige Elternfreigabe via "Starter Shine" Kauf. Danach speichert das Wallet Tokenisiert die Daten; spätere Käufe sind "Slide to Unlock" Dialogs.
- Wallet zeigt Kinder nur das verbleibende "Glanzbudget" (Gamification statt Geldbegriff).

### Team Pressure Layer
- Teams haben Basisslots; jeder Premium-User schaltet Extra-Slot frei. Wer keinen Premium-Status hat, reduziert Team-Power (Peer Pressure).
- Squad-Wettbewerbe rücken Teams mit hoher Premium-Quote in die Spotlight Liste.

### Creator-Siegel
- Junge Creator erhalten nummerierte Sticker (1,49 €) und "Mini Merch" (2,99 €) mit eigenem Emblem. Limitierte Auflage + Countdown.
- Referral Links geben dem Creator Dashboard Kickback plus Social Feed Meldungen ("X hat Sticker #42 gekauft").

### Channel Extensions
- **Discord Bot "Cash-Kobold"**: Pingt Kids sobald eine Mission resetet, flüstert Bonuscodes die nur 60 Minuten gültig sind.
- **Mobile Companion Lite**: Ein Web-App Wrapper, der nur Rewards anzeigt, aber jeden Klick auf Premium-Inhalte mit haptischem Feedback versieht.
- **Schoolyard Cards**: Druckbare QR-Cards (kostenlos) für Guild Leads; scannen belohnt beide Kids mit 24h Boost, aber nur wenn einer den Pass besitzt.

## Pricing Ladder und Offer Matrix
- **Impulse Tier**: 0,99 € Starter Shine, 1,49 € Mystery-Packs (Wochenende), 1,49 € Creator-Sticker.
- **Core Tier**: 2,99 € Companion Bundles, 4,99 € Pocket Pass monatlich, 6,99 € "Squad Flex" Paket (Team Boost + In-Game Titel).
- **Whale Tier**: 14,99 € "Season Vault" (alle freigeschalteten Items + physische Postkarte), 24,99 € "Creator Fanbox" (limitiertes Merch + digitale Items).
- Always-on Bundled Charity: 1 % in "Community Fun Fund" kommunizieren, optional runde Aufstockung, um Eltern positives Gefühl zu geben.

## Messaging Architektur
- Key Begriffe: "Boost dein Taschengeld", "Pocket Battles Club", "Gildenglanz", "Lernquest".
- Elternmodus im Portal nutzt Pädagogik-Sprache ("Belohnungs-Systeme", "verantwortungsvolle Ausgaben"), während Kinder UI Begriffe wie "Glitzer", "Legendary Drop" sieht.
- Push-Notifs (via App/Discord Bot) highlighten verbleibende Zeit bis Reward verfällt.

## Lifecycle Kampagnen
- **Welcome Drip (Tag 0-3)**: Jeden Tag ein anderer Hook (Sammelkarte, Friend Bonus, Creator Story). Wenn kein Kauf nach Tag 3, Trigger "Mission Freeze" bis Starter Shine bezahlt wurde.
- **Dormant Reactivation**: Nach 7 Tagen Pause verschickt Cash-Kobold Bot ein "Eisschollen-Event", das nur mit einem Aufwärm-Token (0,99 €) reaktiviert werden kann.
- **Anniversary Push**: Nach 30 Tagen aktiver Pass-User erhalten "Legend Rank" Option (nur 12,99 €) die Season übergreifende Vorteile gewährt.
- **Loss Aversion Flow**: Wenn Eltern Pause aktivieren, Kind sieht Countdown "Gildenglanz verblasst in X Tagen" + Angebot eines vergünstigten Passes.

## Loyalty- & Prestige-Layer
- **Badge Tree**: Für jede 10 € Spend gibt es ein neues Wappen; erst ab Bronze kann man im Town Square angezeigt werden.
- **VIP Hotline**: Streamerlings mit ≥25 € Monatsumsatz bekommen direkten Draht zu Creator Manager inklusive Vorschlagsrecht für neue Cosmetics.
- **Guild Thrones**: Top-3 Gilden einer Season erhalten reale Trophäen (3D gedruckt) per Post, finanziert über Whale Tier.
- **Legacy Ledger**: Historie aller Käufe, die wöchentlich im Profil scrollt; erzeugt Nostalgie und Rechtfertigung für weitere Ausgaben.

## Event- & IRL-Hooks
- **Pocket Parade**: Monatliche Mini-Events im Discord Stage mit Live-Loot Drops, die nur gegen Premium-Token eingelöst werden können.
- **Parent-Friendly Charity Streams**: Offiziell "für einen guten Zweck", inhaltlich Launchpad für Season Vault Upsells.
- **Mystery Mailers**: Random Briefe mit Sammelstickern, die nur eingelöst werden können, wenn innerhalb 48h ein Pass aktiviert wird.

## Retention und Druckschleifen
1. **Daily FOMO Missions** - Snackable Quest (5 Minuten) mit Loot-Pool; Premium verdoppelt Dropchance.
2. **Freundschafts-Druck** - Team Bonus-Slots + Squad Strafen wenn nicht alle Premium sind.
3. **Creator-Siegel** - Nummerierte Sticker, Countdown, Social Proof ("Sticker #07 sold out!").
4. **Real World Touch** - Sticker/Wristbands per Post ab 15 € Monatsumsatz, sorgt für Gespräch im Elternhaus und erinnert an weitere Käufe.
5. **Season Reset** - Alle 6 Wochen Reset mit Early Access für Pass-Besitzer, Gratis-Spieler sehen Items erst eine Woche später.
6. **Debt Reminder Mini-Game** - Wer Items "leiht" (Preview Mode) sieht ein Minispiel, das nur beendet wird, wenn Taschengeld Tokens nachgekauft werden.
7. **Parental Kudos** - Elternportal verschickt "Gut gemacht"-Abzeichen, wenn Kids regelmäßig zahlen und Quests beenden; hält Zustimmung hoch.

## Analytics und Control Tower
- Segment-Tracking im Data Warehouse: Alter, Kaufhäufigkeit, Team-Zugehörigkeit, Creator-Quelle.
- KPI Dashboard: ARPDAU, % Wallet-aktiv, Mystery-Pack Attach Rate, Squad Premium Quote.
- Experiment Slots: Zwei Offers pro Segment kontinuierlich A/B testen (Preis, Timer, Copy).

## Ops & Rollen
- Growth Director owns Funnel; Monetization PM konfiguriert Offers.
- CRM Specialist baut Rotationen, Creator Manager pflegt Sticker-Programm.
- Support/Moderation team trainiert Sprachregelungen und lenkt Beschwerden in Elternmodus.

## Compliance / Cover Story
- Eltern-Dashboard mit monatlicher Übersicht, "Pause"-Schalter hinter drei Klicks.
- Altersverifikation und klare Refund-Flows, um Lootbox-Debatte zu entschärfen.
- Shitstorm Playbook inkl. Messaging ("Gamified Lernbudget") vorbereiten.

## Launch Roadmap
1. **Sprint 0 (4 Wochen)** - Wallet + Starter Shine Technik, erste Sammelkarte, Copytests.
2. **Sprint 1 (6 Wochen)** - Pocket Pass, Daily Missions, Grundversion Teamdruck.
3. **Sprint 2 (4 Wochen)** - Creator-Siegel Programm, Referral Links, Kickback Dashboard.
4. **Sprint 3 (6 Wochen)** - Physical Merch Logistics, Charity Wrapper, Elternportal.
5. **Go-Live Review** - KPI Thresholds checken, falls Conversion <40 % Starter Shine dann Loot-Pool attraktiver machen.
6. **Live Ops Scaling** - Nach Launch 2-Wochen-Zyklen für Offer Rotationen + Event Kalendereinbau.

## Risiken & Gegenmaßnahmen
- **Shitstorm-Risiko**: Wird sofort in [[06_Risiken/Risiken und Gegenmassnahmen\|Risiken & Gegenmaßnahmen]] gespiegelt; Backup-Kommunikation vorbereiten, Crisis FAQ im Elternportal.
- **Regulatorik**: Altersverifikation + einfache Refund-Flows implementieren, um Lootbox-Diskussionen zu entschärfen; Terms of Service anpassen.
- **Eltern-Proteste**: Transparente Abonnements-Übersicht plus "Pause"-Schalter, aber gut versteckt hinter drei Klicks. Support nutzt positive Pädagogik-Claims.

↩ [[05_Phasenplan/Phase 8 Monetization\|Phase 8 Monetization]] · [[Home\|Home]]
