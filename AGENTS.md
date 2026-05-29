# DkZ AGENTS.md â€” Agenten-Registry

> Stand: 2026-05-30 | Zentrale Agent-Uebersicht fuer alle LLMs

---

## BMAD Agenten (7 Rollen)

| # | Agent | Aufgabe | Status |
|:--|:------|:--------|:-------|
| 1 | Jamesâ„¢ | Guardian â€” ueberwacht alle, coded NICHT | Aktiv (dkz-james.js) |
| 2 | DkZ PMâ„¢ | Product Manager â€” spec.md, User Stories | Definiert |
| 3 | DkZ Architektâ„¢ | plan.md, Tech-Stack | Definiert |
| 4 | DkZ Developerâ„¢ | Coder â€” Ralph-Loop Executor | Definiert |
| 5 | DkZ Reviewerâ„¢ | CodeRabbit â€” Qualitaetspruefung | Definiert |
| 6 | DkZ Testerâ„¢ | Tests + Validierung | TestStrasse v3 |
| 7 | DkZ Dokumentarâ„¢ | README, Wiki, Learnings | Definiert |

---

## NanoBot Fleet

| Bot | Datei | Zweck |
|:----|:------|:------|
| Antigravity | nanobot-antigravity.js | Gemini Agent Kommunikation |
| OpenCode | nanobot-opencode.js | OpenCode Agent Kommunikation |

---

## Health Check System

| Komponente | Zweck |
|:-----------|:------|
| Startup Skill | Session-Start Validierung |
| Checkup Skill | Deep Diagnostik |
| Health Agent | Universeller Pruefer |
| Health Chain | Python Check-Kette |
| REDNOTE DB | Zentrale Fehlerdatenbank |
| REDNOTE Collector | Fehler-Manager CLI |
| Dashboard | Visueller Health Monitor |

---

## Skills (54 Skills in .agents/skills/)

### Kern-Skills
- startup â€” Session-Start Check
- checkup â€” Deep Diagnostik
- health-agent â€” Universeller Pruefer
- power â€” Superpowers Lab + DDD
- power-openspec â€” OpenSpec Integration
- playbook â€” Regeln und Playbooks laden

### Entwicklungs-Skills
- mod-builder â€” Modul Generator
- dkz-webapp-builder â€” WebApp Builder
- dkz-skillpack â€” Skill-Paket Manager
- ralph-loop-tester â€” Ralph Loop Tests
- react-components â€” Stitch zu React

### Content-Skills
- notebooklm-integration â€” NLM Batch Content
- frontpage-builder â€” Landing Pages
- changelog-generator â€” Changelogs
- swarm-content-creator â€” Multi-Agent Content

### Design-Skills
- stitch-design â€” Stitch Design System
- taste-design â€” Semantic Design
- hyperreal-ui â€” Hyperrealistisches UI
- enhance-prompt â€” Prompt Enhancement

---

## Kommunikation

```
Agent <-> NanoChat Bridge (Port 3040) <-> Dashboard
  |                                        |
REDNOTE.json                          localStorage
```

Alle Agenten kommunizieren ueber die NanoChat Bridge.
Health-Checks laufen ueber die Python Chain oder Shell-Befehle.
