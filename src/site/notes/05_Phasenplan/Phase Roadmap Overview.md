---
{"dg-publish":true,"permalink":"/05-phasenplan/phase-roadmap-overview/"}
---

# Phase Roadmap Overview

> Übersicht mit Verantwortlichen, Status & wichtigen Terminen. Aktualisiere die Frontmatter jeder Phase bei Meetings; die Tabelle rendert sich automatisch via Dataview.

```dataview
TABLE
  "[[" + file.name + "]]" AS Phase,
  period AS "Zeitraum",
  focus AS "Focus",
  primary_owner AS "Primary Owner",
  secondary_owner AS "Secondary",
  status_icon + " " + status AS "Status",
  join(milestones, ", ") AS "Key Milestones"
FROM "05_Phasenplan"
WHERE phase >= 0 AND phase <= 9
SORT phase ASC
```

> Status-Legende: 🟢 planning/done · 🟠 in-progress · ⏳ upcoming · 🔴 blocked

↩ [[Home\|Home]]
