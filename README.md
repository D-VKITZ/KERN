# DEVKiTZ KERN

> Zentrales Repository fuer Rules, Playbook, Patterns, Templates und Dokumentation.
> Jedes LLM findet hier direkt alle Verweise.

---

## Inhalt

| Datei | Beschreibung |
|:------|:-------------|
| llms.txt | LLM Navigation - 152+ Module, 53 Skills, 77 Workflows |
| RULES.md | 10 Eiserne Regeln |
| AGENTS.md | 7 BMAD Agenten + NanoBot Fleet |
| PLAYBOOK.md | Session Start + Build + Deploy Workflow |
| PATTERNS.md | 12 Design Patterns mit Code-Beispielen |
| SYNTAX.md | HTML/CSS/JS/Git Coding Standards |
| TEMPLATES.md | 5 Templates (HTML, CSS, Agent, Workflow, README) |
| VPS_TASKS.md | VPS Tasks P1-P3 mit Status |
| scripts/vps-auto-update.py | Auto-Update Pipeline (Cron) |

---

## Quick Navigation

### Oekosystem

- **Dashboard:** 152+ Module - devkitz.sites
- **GitHub:** github.com/D-VKITZ (29 Repos) + github.com/7IKED
- **VPS:** KVM8 (Docker Compose) + EU Cloud (geplant)

### Agenten

7 BMAD Agenten: James Guardian, PM, Architekt, Developer, Reviewer, Tester, Dokumentar

### Design

Neon Matrix: schwarz (#000000) + neon-gruen (#00ff88) + accent (#fa1e4e)

### Tech

Vanilla HTML5/CSS3/JS ES6+ (Dashboard) + Optional React/Vite (PWA Apps)

---

## VPS Auto-Update

```bash
# Cron Setup auf VPS
0 */4 * * * /usr/bin/python3 /opt/devkitz/scripts/vps-auto-update.py >> /var/log/devkitz-update.log 2>&1
```

Pipeline: Git Pull -> features.json -> llms.txt -> Deploy rsync -> Git Push

---

## Kanban Boards

| # | Board | Projekt |
|:--|:------|:--------|
| 1 | Dashboard Modules | #13 |
| 2 | VPS Infrastructure | #14 |
| 3 | Design System | #15 |
| 4 | Agent Kanban | #16 |
| 5 | Abteilungen | #17 |
| 6 | Templates Hub | #18 |
| 7 | Pattern Library | #19 |

---

## Issues Status (Live)

| Prio | Issue | Status |
|:-----|:------|:-------|
| P1 | vLLM Auth Fix #208 | OPEN |
| P1 | Telegram Bot #209 | OPEN |
| P2 | Blogger API #210 | OPEN |
| P2 | Google Photos #211 | OPEN |
| P2 | Docker Health #212 | OPEN |
| P2 | SSL Certs #213 | OPEN |
| P3 | EU Cloud VPS #214 | OPEN |
| P3 | Immich #215 | OPEN |
| P3 | Paperless #216 | OPEN |
| P3 | n8n Workflows #217 | OPEN |

---

DEVKiTZ - Made by 777 - 2026