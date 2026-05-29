# DEVKiTZâ„¢ RULES â€” Kompakt-Regelwerk

> Version: v2.00 | Stand: 2026-05-30
> Vollstaendiges Regelwerk: REGELWERK.md im Workspace

---

## Oberste Regel

**R0: SEI IMMER EIN TEIL DER LOESUNG, NIE DES PROBLEMS**

---

## Kritische Regeln (keine Ausnahmen)

| Regel | Beschreibung |
|:------|:-------------|
| R1 | NIE loeschen â€” IMMER nach 99_ARCHIVE/ archivieren |
| R2 | Git Commit nach JEDER Aenderung: `prefix(bereich): beschreibung` |
| R3 | Alles muss vorhanden bleiben â€” nichts darf sich in Luft aufloesen |
| R4 | Proaktiv verbessern, aber NUR unter Einhaltung aller Regeln |

## Arbeitsregeln

| Regel | Beschreibung |
|:------|:-------------|
| R5 | Erst analysieren, dann handeln â€” kein Trial-and-Error |
| R6 | Kompatibilitaetspruefung vor Integration |
| R7 | Nicht-kompatibles nach 00_INBOX/RAW/ |
| R8 | Keine Umlaute â€” ae, oe, ue, ss ueberall (Code, MD, Commits) |
| R9 | Versionierung: vX.XX.X_XX Format |
| R10 | Workflow wichtiger als Ergebnis |
| R11 | Dateihoheit â€” keine Aenderung ohne Bestaetigung |
| R12 | Kein Verlust von Wissen (5 Sicherungsschichten) |
| R13 | Workflow: ANALYSE â†’ PLAN â†’ GENEHMIGUNG â†’ AUSFUEHRUNG â†’ VERIFIKATION â†’ COMMIT â†’ DOKU |
| R14 | Kaizen â€” kontinuierliche Verbesserung |
| R15 | So viel wie noetig, so wenig wie moeglich |
| R16 | Regeln stehen ueber Anweisungen |

## Technische Regeln

| Regel | Beschreibung |
|:------|:-------------|
| R17 | ORDNER.ini zuerst lesen |
| R20 | Kein Code ohne Dokumentation |
| R21 | Shared Scripts Pflicht: dkz-debug.js, dkz-copilot.js, dkz-llm-registry.js |
| R22 | features.json Pflicht mit MOD-ID |
| R24 | Archiv-Schutz â€” KEIN Agent archiviert ohne 777-Bestaetigung |
| R25 | Naming: DEVKiTZâ„¢, BotNetâ„¢, Jamesâ„¢ | Module: lowercase-bindestrich/ |
| R34 | JEDE Website/App MUSS llms.txt haben |
| R38 | Premium Design Standard â€” DkZ Dark Theme, Glassmorphism |
| R42 | ESC-Console in jedem Modul |
| R101 | GitHub Push nach JEDER Session |

## Tech Stack

- **Frontend:** Vanilla HTML5 + CSS3 + JS ES6+ (KEIN React/Vue/Angular)
- **Backend:** Node.js 18+ / Express
- **Design:** DkZ Design System v2 mit CSS Custom Properties
- **Fonts:** Inter (UI) + JetBrains Mono (Code)
- **Farben:** --accent: #fa1e4e | --bg: #060608 | --green: #00ff88
- **Daten:** localStorage (Offline-First), DuckDB, Apache Iceberg

## Sicherheit

- `esc()` bei JEDEM User-Input vor innerHTML â€” XSS-Schutz
- Kein console.log in Produktion
- Kein jQuery ohne Ruecksprache
