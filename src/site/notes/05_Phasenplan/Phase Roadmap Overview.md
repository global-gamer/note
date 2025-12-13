---
{"dg-publish":true,"permalink":"/05-phasenplan/phase-roadmap-overview/","dgPassFrontmatter":true,"noteIcon":"","created":"2025-12-08T18:36:50.133+01:00","updated":"2025-12-13T14:41:39.202+01:00"}
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
