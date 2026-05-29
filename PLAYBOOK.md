# DEVKiTZâ„¢ PLAYBOOK â€” Kompakt-Version

> Methodik, Workflows und Best Practices fuer das DkZ Oekosystem.
> Vollstaendiges Playbook: 04_SYSTEM/DKZ_PLAYBOOK.md (~105 KB)

---

## BMADâ„¢ Methodik (7 Agenten)

**Blueprint â†’ Mapping â†’ Analyse â†’ Design**

| # | Agent | Aufgabe |
|:--|:------|:--------|
| 1 | Jamesâ„¢ | Guardian â€” ueberwacht alle, coded NICHT |
| 2 | DkZ PMâ„¢ | Product Manager â€” spec.md, User Stories |
| 3 | DkZ Architektâ„¢ | plan.md, Tech-Stack Entscheidungen |
| 4 | DkZ Developerâ„¢ | Coder â€” Ralph-Loop Executor |
| 5 | DkZ Reviewerâ„¢ | CodeRabbit â€” Qualitaetspruefung |
| 6 | DkZ Testerâ„¢ | Tests + Validierung (TestStrasse v3) |
| 7 | DkZ Dokumentarâ„¢ | README, Wiki, Learnings |

---

## Ralph-Loopâ„¢ (6 Phasen)

```
1. LESEN    â†’ prd.json + constitution + AGENTS.md
2. SPAWN    â†’ Neue Instanz (frischer Kontext!)
3. EXECUTE  â†’ Developer schreibt Code
4. VERIFY   â†’ Tester/Reviewer prueft
5. COMMIT   â†’ Git commit + prd.json update
6. LOOP     â†’ Naechster Task
```

**Kernprinzip:** Jeder Task bekommt frischen Kontext â€” kein Context Drift!

---

## Workflow-Kette (R13)

```
ANALYSE â†’ PLAN â†’ GENEHMIGUNG â†’ AUSFUEHRUNG â†’ VERIFIKATION â†’ COMMIT â†’ DOKUMENTATION
```

---

## Session-Ablauf

### Start
1. LLM_BOOTSTRAP.md lesen
2. CLAUDE.md oder GEMINI.md lesen
3. `git log -5` pruefen
4. Begruessungsprotokoll

### Ende
1. features.json aktualisiert?
2. Git committed + pushed?
3. Walkthrough/Notes gespeichert?
4. WissenHub archiviert?

---

## Modul-Erstellung

1. Ordner: `modules/kebab-case/`
2. `index.html` mit DkZ Design System
3. `features.json` mit MOD-ID
4. Shared Scripts einbinden (R21)
5. REGISTRY.json aktualisieren
6. BLAUPAUSE.md aktualisieren
7. Git commit

---

## Design Standards (R38)

- DkZ Dark Theme (#060608 Background)
- Glassmorphism mit Micro-Animations
- Inter (UI) + JetBrains Mono (Code)
- CSS Custom Properties (--accent: #fa1e4e)
- esc() bei jedem User-Input (R21)
- ESC-Console in jedem Modul (R42)

---

## LLM Routing

- Flash/Nano (80%): Heartbeat, Routing, Quick Lookups
- Standard: Normale Aufgaben
- Premium: Komplexe Analyse, Code Generation
- Ziel: 60-90% Kosten sparen

---

## Sicherungsschichten (R12)

1. Git History
2. 99_ARCHIVE/
3. 02_RESEARCH/
4. 00_INBOX/RAW/
5. [DEEPKEEP]

---

## Artefakt-Typen

| Typ | Tag | Beschreibung |
|:----|:----|:-------------|
| Task | task | Checkliste, Fortschritt |
| Walkthrough | walkthrough | Nachweis, Screenshots |
| Implementierungsplan | impl-plan | Technischer Plan |
| Blaupause | blueprint | Architektur, Design |
| Scratchpad | scratch | Notizen, Ideen |
| Research | research | Recherche, Analyse |
| Report | report | Status-Berichte, Metriken |

---

## KI-Tooling

- OpenClawâ„¢ â€” AI Coding Assistant
- PicoClawâ„¢ â€” Lightweight AI
- BMADâ„¢ â€” Multi-Agent Framework
- CodeRabbit â€” Automated Code Review
- NanoChat â€” Flash/Nano Modelle (~$0.01/1M Tokens)

---

*Kompakt-Version. Vollstaendig: 04_SYSTEM/DKZ_PLAYBOOK.md*
