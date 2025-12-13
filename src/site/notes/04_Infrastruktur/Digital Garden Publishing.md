---
{"dg-publish":true,"permalink":"/04-infrastruktur/digital-garden-publishing/"}
---

# Digital Garden Publishing (Obsidian)

Wir verwenden das Obsidian-Plugin **Digital Garden** als Publishing-Layer. Die wichtigsten Punkte aus den Plugin-Dokumentationen sind hier zusammengefasst, damit jeder ohne Git-Kenntnisse Notes veröffentlichen kann.

## Setup & Voraussetzungen
1. **Plugin installieren** (Community Plugins → „Digital Garden“). Aktivieren und Obsidian neu starten.
2. **GitHub Repo angeben** – Plugin fragt nach `username/digitalgarden` + Branch (standardmäßig `main`). Dieses Repo hostet die generierten Seiten (GitHub Pages, Vercel o. ä.).
3. **Personal Access Token** mit Repo-Rechten erstellen und im Plugin speichern (Secure Storage). Token erlaubt dem Plugin, Markdown → JSON → Repo push zu machen.
4. **Garden Settings**:
   - `Site Name`, `Site Base URL`, Footer, etc.
   - Assets (z. B. `garden.css`, Javascript) können später optional überschrieben werden.

## Frontmatter Controls
| Feld | Bedeutung | Nutzung bei uns |
| --- | --- | --- |
| `dg-publish: true` | Checkbox (Obsidian) die Note zur Veröffentlichung markiert. | Bereits in **allen** Notes gesetzt. |
| `dg-home: true` | Definiert die Startseite des Digital Garden. | `Home.md` ist unser Garden-Root. |
| `dg-path: phases/phase-7` | Optionaler virtueller Ordner/Slug. | Verwenden, wenn Web-URL nicht Ordnerstruktur folgen soll. |
| `dg-permalink: monetization/phase7` | Individuelle URL, überschreibt `dg-path`. |
| `dg-title: ...` | Überschrift auf der Website überschreiben (falls Markdown-Titel nicht passt). |
| `dg-description: ...` | Kurzer Text für SEO/Preview (erscheint im HTML `<meta>`). |
| `dg-pinned: true` | Note wird im linken Menü immer angezeigt. |
| `dg-hide: true` | Note bleibt veröffentlicht, aber erscheint nicht in Listen/Graph. |
| `dg-tags: [\"phase\", \"monetization\"]` | Zusätzliche Tags für die Garden-Filter (optional). |
| `dg-icon: rocket` | Legt das Icon in der linken Navigation fest (FontAwesome/Friendly). |
| `dg-metadata:` | YAML-Block für Key/Value-Tabellen oben auf der Seite. |

> Checkboxen wie `dg-publish`, `dg-home`, `dg-pinned`, `dg-hide` erscheinen automatisch als schaltbare Felder im Frontmatter-Panel von Obsidian.

## Publishing-Workflow
1. Note erstellen/aktualisieren.
2. Sicherstellen, dass `dg-publish` aktiviert ist (Standard) und sich keine vertraulichen Daten darin befinden.
3. Optional `dg-path` oder `dg-permalink` setzen, falls eine sprechendere URL gebraucht wird.
4. In Obsidian Command Palette:
   - `Digital Garden: Publish Single Note` → nur aktuelle Note.
   - `Digital Garden: Publish Multiple Notes` → Batch (z. B. gesamte Kategorie).
   - `Digital Garden: Publish All Notes` → kompletter Sync.
5. Plugin pushed geänderte Dateien ins GitHub Repo → Hosting (GitHub Pages/Vercel) deployed automatisch.

## Empfohlene Konventionen
- **Home**: Nur `Home.md` besitzt `dg-home: true` (bereits gesetzt). Alle anderen Notes bleiben regulär verlinkt.
- **Pfadsteuerung**: Für strukturierte URLs (z. B. `/phasen/phase-7`) `dg-path` nutzen; falls Slug eindeutig sein soll, `dg-permalink`.
- **Pinned Navigation**: Wichtige Übersichtsseiten (Home, Vision, Phasenplan) können `dg-pinned: true` + `dg-icon` erhalten, damit die linke Navigation des Garden strukturierter wirkt.
- **SEO/Inhalt**: Bei öffentlichen Artikeln `dg-description` sowie `dg-tags` pflegen; optional `dg-metadata` mit Owner, Phase, Status etc. anzeigen.
- **Draft Handling**: Notes, die nicht in den Garden sollen, behalten `dg-publish: false` oder man entfernt den Frontmatter-Block komplett (dann sind sie privat).

## To-Do / Next Steps
- [ ] Plugin-Settings in Obsidian setzen (Repo, Token, Base URL).
- [ ] Entscheiden, welche Notes `dg-pinned` und `dg-icon` bekommen (Home, Vision, Phasenplan).
- [ ] Optional `dg-path`/`dg-permalink` vergeben, falls URLs von der Ordnerstruktur abweichen sollen.
- [ ] Eigene Styles (`garden.css`) bzw. JS-Hooks definieren, um Branding aus [[04_Infrastruktur/Domains und Branding\|Domains und Branding]] zu übernehmen.
- [ ] Publishing-Checklist im [[Templates/Meeting-Template\|Templates/Meeting-Template]] ergänzen (Status „Garden Sync OK?“).

↩ [[Home\|Home]] · Weitere Infos direkt im Plugin („Digital Garden > Help & Documentation“).
