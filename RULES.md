# DEVKiTZ Rules (Kompakt)

## Eiserne Regeln

1. esc() bei JEDEM User-Input vor innerHTML - XSS-Schutz
2. DkZ CSS Variables - kein Hardcoded hex
3. Shared Scripts einbinden: dkz-debug, dkz-copilot, dkz-james, dkz-navbar, dkz-console, dkz-premium
4. features.json nach Modul-Aenderung aktualisieren
5. Git Commit nach JEDER Aenderung
6. NIE loeschen - IMMER archivieren 99_ARCHIVE/
7. Dashboard Module: Vanilla Only - PWA Apps: React optional
8. Skills IMMER pruefen BEVOR Aktion
9. llms.txt in jedem Verzeichnis pflegen
10. Keine Umlaute: ae, oe, ue, ss

## Tech Stack

- Frontend: Vanilla HTML5 + CSS3 + JS ES6+
- PWA: Optional React + Vite + Tailwind
- Design: --bg:#000 --green:#00ff88 --accent:#fa1e4e
- Fonts: Inter + JetBrains Mono
- Daten: localStorage, DuckDB, Iceberg

## Format

- Commits: feat(bereich): beschreibung
- Module: lowercase-bindestrich/
- Shared: dkz-funktion.js
- Docs: .md
- Config: .json