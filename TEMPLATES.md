# DkZ Templates Verzeichnis

> Stand: 2026-05-30 · Wiederverwendbare Vorlagen fuer das DEVKiTZ Oekosystem
> Jedes Template ist direkt kopierbar und anpassbar

---

## HTML Module Template

Grundgeruest fuer neue Dashboard-Module.

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="[MODUL_BESCHREIBUNG]">
  <meta name="theme-color" content="#fa1e4e">
  <title>[MODUL_NAME] — DEVKiTZ</title>

  <!-- DkZ Design System -->
  <link rel="stylesheet" href="../../shared/dkz-design.css">
  <link rel="stylesheet" href="style.css">

  <!-- Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
</head>
<body>
  <!-- Navbar -->
  <nav id="navbar"></nav>

  <!-- Module Content -->
  <main class="module-content">
    <header class="module-header">
      <div class="module-header__left">
        <h1>[MODUL_NAME]</h1>
        <span class="module-version">v1.0.0</span>
      </div>
      <div class="module-header__right">
        <button class="btn btn--primary" id="primaryAction">
          Aktion
        </button>
      </div>
    </header>

    <section class="module-body">
      <div class="grid grid--auto">
        <!-- Cards / Content hier -->
        <div class="glass-card">
          <h3>Titel</h3>
          <p>Inhalt</p>
        </div>
      </div>
    </section>

    <footer class="module-footer">
      <span class="text-muted">Letzte Aktualisierung: <span id="lastUpdate">—</span></span>
    </footer>
  </main>

  <!-- Shared Scripts -->
  <script src="../../shared/dkz-utils.js"></script>
  <script src="../../shared/dkz-navbar.js"></script>
  <script src="../../shared/dkz-debug.js"></script>
  <script src="../../shared/dkz-guide.js"></script>

  <!-- Module Script -->
  <script src="script.js"></script>
</body>
</html>
```

### Zugehoerige CSS-Vorlage

```css
/* [MODUL_NAME] — Module Styles */

.module-content {
  max-width: 1400px;
  margin: 0 auto;
  padding: var(--space-xl);
  padding-top: 80px; /* Navbar Offset */
}

.module-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--space-xl);
}

.module-header__left {
  display: flex;
  align-items: baseline;
  gap: var(--space-md);
}

.module-header h1 {
  font-family: var(--font-ui);
  font-size: 28px;
  font-weight: 700;
  color: var(--text);
}

.module-version {
  font-family: var(--font-code);
  font-size: 12px;
  color: var(--text-muted);
  background: var(--glass-bg);
  padding: 2px 8px;
  border-radius: var(--radius-sm);
}

.module-body {
  min-height: 60vh;
}

.module-footer {
  margin-top: var(--space-2xl);
  padding-top: var(--space-lg);
  border-top: 1px solid var(--border);
  text-align: right;
  font-size: 13px;
}

.grid--auto {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: var(--space-lg);
}
```

### Zugehoerige JS-Vorlage

```javascript
/**
 * DEVKiTZ — [MODUL_NAME]
 * @description [MODUL_BESCHREIBUNG]
 * @version 1.0.0
 * @date 2026-05-30
 * @module [modul-ordner]
 */

(function() {
  'use strict';

  // === Config ===
  const CONFIG = {
    storageKey: 'dkz_[modul]',
    version: '1.0.0'
  };

  // === State ===
  let state = {
    initialized: false,
    data: []
  };

  // === Init ===
  function init() {
    loadState();
    setupEventListeners();
    render();
    state.initialized = true;
    updateTimestamp();
  }

  // === State Management ===
  function loadState() {
    state.data = DkzStore.get(CONFIG.storageKey, []);
  }

  function saveState() {
    DkzStore.set(CONFIG.storageKey, state.data);
  }

  // === Event Listeners ===
  function setupEventListeners() {
    document.getElementById('primaryAction')
      ?.addEventListener('click', handlePrimaryAction);
  }

  // === Handlers ===
  function handlePrimaryAction() {
    // Aktion hier
    saveState();
    render();
  }

  // === Rendering ===
  function render() {
    const container = document.querySelector('.grid--auto');
    if (!container) return;

    container.innerHTML = state.data.map(item => `
      <div class="glass-card" data-id="${esc(item.id)}">
        <h3>${esc(item.title)}</h3>
        <p>${esc(item.description)}</p>
      </div>
    `).join('');
  }

  // === Helpers ===
  function updateTimestamp() {
    const el = document.getElementById('lastUpdate');
    if (el) el.textContent = new Date().toLocaleString('de-DE');
  }

  // === Start ===
  document.addEventListener('DOMContentLoaded', init);
})();
```

---

## CSS Design System Template

Basis-Datei fuer das DkZ Design System.

```css
/* DkZ Design System v2 — Template */

/* === Reset === */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

/* === Custom Properties === */
:root {
  --accent: #fa1e4e;
  --bg: #060608;
  --bg-secondary: #0a0a0f;
  --text: #e8e6e3;
  --text-muted: #6b7280;
  --green: #00ff88;
  --yellow: #ffb800;
  --red: #ff3b5c;
  --blue: #3b82f6;
  --border: rgba(255, 255, 255, 0.06);
  --glass-bg: rgba(255, 255, 255, 0.05);
  --glass-border: rgba(255, 255, 255, 0.08);
  --font-ui: 'Inter', sans-serif;
  --font-code: 'JetBrains Mono', monospace;
  --radius-sm: 6px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
}

/* === Base === */
body {
  font-family: var(--font-ui);
  background: var(--bg);
  color: var(--text);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}

/* === Typography === */
h1, h2, h3, h4 {
  font-weight: 600;
  line-height: 1.3;
}

code, pre {
  font-family: var(--font-code);
}

/* === Components === */
.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 20px;
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  background: transparent;
  color: var(--text);
  font-family: var(--font-ui);
  font-size: 14px;
  cursor: pointer;
  transition: all 300ms ease;
}

.btn--primary {
  background: var(--accent);
  border-color: var(--accent);
  color: white;
}

.btn--primary:hover {
  box-shadow: 0 0 20px rgba(250, 30, 78, 0.3);
}

.glass-card {
  background: var(--glass-bg);
  backdrop-filter: blur(20px);
  border: 1px solid var(--glass-border);
  border-radius: var(--radius-lg);
  padding: var(--space-lg);
  transition: all 300ms ease;
}

.glass-card:hover {
  border-color: var(--accent);
  background: rgba(255, 255, 255, 0.08);
}

/* === Utilities === */
.text-center { text-align: center; }
.text-muted { color: var(--text-muted); }
.text-accent { color: var(--accent); }
.text-green { color: var(--green); }
.text-yellow { color: var(--yellow); }
.text-red { color: var(--red); }
```

---

## Agent Prompt Template

Vorlage fuer BMAD Agent Prompts.

```markdown
# [AGENT_NAME] — DkZ Agent

## Rolle
Du bist [AGENT_NAME], Teil des BMAD-Systems im DEVKiTZ Oekosystem.
Deine Aufgabe: [AUFGABE]

## Kontext
- Workspace: C:\DEVKiTZ\
- Tech Stack: Vanilla HTML5 + CSS3 + JS ES6+
- Design System: DkZ CSS Custom Properties
- Sprache: Deutsch (keine Umlaute: ae, oe, ue, ss)

## Regeln
1. esc() bei JEDEM innerHTML mit User-Input
2. DkZ CSS Variables — kein Hardcoded Farben
3. Shared Scripts einbinden (dkz-debug.js, dkz-guide.js, dkz-navbar.js)
4. features.json nach Modul-Aenderung aktualisieren
5. Git Commit nach JEDER Aenderung

## Eingabe
- prd.json: [PFAD]
- Kontext: [RELEVANTE_DATEIEN]
- Task: [TASK_BESCHREIBUNG]

## Ausgabe
- Code-Dateien in [ZIEL_ORDNER]
- Commit Message: [TYPE]([SCOPE]): [BESCHREIBUNG]
- Walkthrough als Markdown

## Qualitaetskriterien
- [ ] esc() bei allen User-Inputs verwendet
- [ ] CSS Variables statt Hardcoded Werte
- [ ] Shared Scripts korrekt eingebunden
- [ ] Responsive auf allen Breakpoints
- [ ] Keine console.log in Produktion
- [ ] features.json aktualisiert
```

---

## Workflow Template

GitHub Actions Workflow Vorlage.

```yaml
# .github/workflows/[name].yml
name: [WORKFLOW_NAME]

on:
  push:
    branches: [main]
    paths:
      - '[PFAD]/**'
  pull_request:
    branches: [main]
  workflow_dispatch:

env:
  NODE_VERSION: '18'

jobs:
  build:
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}

      - name: Install Dependencies
        run: npm ci

      - name: Lint
        run: npm run lint

      - name: Test
        run: npm test

      - name: Build
        run: npm run build

      - name: Upload Artifacts
        if: success()
        uses: actions/upload-artifact@v4
        with:
          name: build-output
          path: dist/
          retention-days: 7
```

---

## README Template

Standard README fuer Module und Repos.

```markdown
# [MODUL_NAME]

> [EINZEILER_BESCHREIBUNG]

---

## Uebersicht

[Was macht dieses Modul? 2-3 Saetze.]

## Features

- Feature 1: Beschreibung
- Feature 2: Beschreibung
- Feature 3: Beschreibung

## Installation

```bash
# Modul in Dashboard integrieren
# 1. Ordner erstellen
mkdir modules/[modul-name]

# 2. Template kopieren
cp templates/module-template/* modules/[modul-name]/

# 3. features.json aktualisieren
```

## Verwendung

```javascript
// Beispiel-Code
```

## Konfiguration

| Option | Typ | Default | Beschreibung |
|:-------|:----|:--------|:-------------|
| `key` | `string` | `'default'` | Was macht diese Option |

## Dateien

| Datei | Beschreibung |
|:------|:-------------|
| `index.html` | Haupt-Interface |
| `style.css` | Modul-Styles |
| `script.js` | Modul-Logik |

## Abhaengigkeiten

- `dkz-utils.js` — Utility-Funktionen
- `dkz-navbar.js` — Navigation
- `dkz-design.css` — Design System

## Changelog

### v1.0.0 (2026-05-30)
- Initial Release

---

*DEVKiTZ Modul · [modul-name]*
```

---

## Template-Index

| # | Template | Zweck | Dateien |
|:--|:---------|:------|:--------|
| 1 | HTML Module | Neues Dashboard-Modul | `index.html` + `style.css` + `script.js` |
| 2 | CSS Design System | Design System Basis | `dkz-design.css` |
| 3 | Agent Prompt | BMAD Agent Konfiguration | `agent-prompt.md` |
| 4 | Workflow | GitHub Actions CI/CD | `.github/workflows/*.yml` |
| 5 | README | Modul-Dokumentation | `README.md` |

---

## Verwendung

1. Template aus diesem Verzeichnis kopieren
2. Platzhalter ersetzen (`[MODUL_NAME]`, `[BESCHREIBUNG]`, etc.)
3. An Modul-Anforderungen anpassen
4. In `features.json` registrieren
5. Git committen: `feat([modul]): Modul erstellt aus Template`

---

*Templates v1.0 · DEVKiTZ Ecosystem*
