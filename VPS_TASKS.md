# DEVKiTZ VPS Tasks + Mindmaps

## VPS Infrastruktur

KVM8 Primary (195.XXX) -> Docker Compose
  vLLM :8811 | n8n :5678 | Telegram Bot
  Watchtower | nginx | certbot

EU Cloud Plan -> Puter VPS
  Immich :2283 | Paperless | Playwright
  CC Workflow | OpenSwarm

GitHub Pages -> devkitz.sites
  Dashboard | Wiki | Modules (152+)

## Agenten (BMAD 7 Rollen)

James Guardian > Health Monitor Score 0-100
PM > User Stories PRD.json
Architekt > Tech Stack Design
Developer > Ralph Loop 6 Phase
Reviewer > Quality Gates Patterns
Tester > TestStrasse v3 50+ Checks
Dokumentar > README Wiki Learnings

## VPS Tasks

P1.1 vLLM Auth Fix #208 - VLLM_API_KEY env var
P1.2 Telegram Bot Token #209 - BotFather
P2.1 Blogger API Key #210 - GCP Console
P2.2 Google Photos OAuth #211 - Photos Library API
P2.3 SSL Zertifikate #213 - certbot renew
P2.4 Docker Health #212 - docker ps
P3.1 EU Cloud VPS #214 - Puter 15 EUR/Monat
P3.2 Immich #215 - Docker Compose
P3.3 Paperless-ngx #216 - OCR System
P3.4 n8n Workflows #217 - Auto-Backup Health Blog Git

## Auto-Update Pipeline

Cron 4h > Git Pull > features.json > llms.txt > Deploy rsync > Push
Script: 04_SYSTEM/scripts/vps-auto-update.py
Kein lokaler Rechner noetig