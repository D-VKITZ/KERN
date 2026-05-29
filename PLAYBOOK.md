# DEVKiTZ Playbook (Kompakt)

## Session Start
1. LLM_BOOTSTRAP.md lesen
2. GEMINI.md oder CLAUDE.md lesen
3. git log -5 pruefen
4. Begruessungsprotokoll

## Build Workflow
1. Plan: Was wird gebaut?
2. Design: DkZ CSS Variables
3. Code: Vanilla HTML/CSS/JS
4. Shared Scripts einbinden
5. Test: features.json + Health
6. Commit: feat(bereich): desc
7. Push: git push origin main

## Module erstellen
1. mkdir modules/modul-name/
2. index.html erstellen
3. esc() bei innerHTML
4. Shared Scripts einbinden
5. features.json aktualisieren
6. Hub-Link einbauen
7. Git commit + push

## Qualitaet
- Kein console.log
- Kein jQuery
- Keine Umlaute
- esc() IMMER
- DkZ CSS Variables IMMER
- EN/DE Toggle wenn moeglich
- Kontrast-Modus wenn moeglich

## Deployment
- Dashboard: GitHub Pages devkitz.sites
- API: VPS KVM8 Port 3040
- VPS Auto-Update: Cron alle 4h