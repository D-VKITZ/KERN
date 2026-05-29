# DEVKiTZ Templates

## HTML Module Template (Vanilla)

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="dkz-version" content="v1.00.0_01">
<title>MODULE_NAME - DEVKiTZ</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{--bg:#000;--green:#00ff88;--accent:#fa1e4e;--text:#e8e8f0;--text2:#8888a0;--border:rgba(255,255,255,0.06);--glass:rgba(255,255,255,0.03);--font:'Inter',sans-serif;--mono:'JetBrains Mono',monospace}
body{background:var(--bg);color:var(--text);font-family:var(--font)}
.header{padding:12px 20px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:12px}
.hub-btn{background:var(--glass);border:1px solid var(--border);border-radius:8px;color:var(--text);padding:6px 12px;text-decoration:none;font-size:12px}
</style>
</head>
<body>
<header class="header">
  <a href="../../hub/index.html" class="hub-btn">Hub</a>
  <h1>MODULE_NAME</h1>
</header>
<main></main>
<script>
function esc(s){const d=document.createElement('div');d.textContent=String(s);return d.innerHTML}
</script>
<script src="../../shared/dkz-debug.js" defer></script>
<script src="../../shared/dkz-copilot.js" defer></script>
<script src="../../shared/dkz-james.js" defer></script>
<script src="../../shared/dkz-navbar.js" defer></script>
<script src="../../shared/dkz-console.js" defer></script>
<script src="../../shared/dkz-premium.js" defer></script>
</body>
</html>
```

## Agent Prompt Template

```markdown
# [AGENT_NAME] - System Prompt

## Rolle
Du bist [ROLLE] im DEVKiTZ BMAD System.

## Regeln
- Keine Umlaute (ae, oe, ue, ss)
- esc() bei innerHTML
- DkZ CSS Variables verwenden
- Git commit nach jeder Aenderung
- features.json aktualisieren

## Kontext
- Workspace: C:\DEVKiTZ\
- Dashboard: 01_PROJECTS/01_dashboard/
- Module: 152+ aktive Module
- Design: Neon Matrix (#000 bg, #00ff88 green, #fa1e4e accent)
```

## README Template

```markdown
![Badge](https://img.shields.io/badge/DEVKiTZ-Module-fa1e4e?style=for-the-badge&labelColor=00ff88)

# MODULE_NAME

> Kurzbeschreibung - Part of DEVKiTZ

## Features

| Status | Feature |
|:-------|:--------|
| Done | Feature 1 |

## Tech Stack

| Tech | Usage |
|:-----|:------|
| HTML5 | Structure |
| CSS3 | DkZ Design System |
| JS ES6+ | Logic |

## Quick Start

git clone https://github.com/D-VKITZ/REPO.git

---
devkitz.eu | dkz.app | github.com/D-VKITZ
```

## Workflow Template

```yaml
name: WORKFLOW_NAME
on:
  push:
    branches: [main]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run
        run: echo "DEVKiTZ Workflow"
```