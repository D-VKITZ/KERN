# DkZ Coding Standards

> Stand: 2026-05-30 · Verbindliche Syntax- und Formatierungsregeln
> Gilt fuer ALLE Dateien im DEVKiTZ Oekosystem

---

## HTML Standards

### Semantic Tags

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="DEVKiTZ Modul Beschreibung">
  <meta name="theme-color" content="#fa1e4e">
  <title>Modul Name — DEVKiTZ</title>

  <!-- DkZ Design System -->
  <link rel="stylesheet" href="../../shared/dkz-design.css">
  <link rel="stylesheet" href="style.css">

  <!-- Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
</head>
<body>
  <nav id="navbar"></nav>

  <main class="module-content">
    <header class="module-header">
      <h1>Modul Name</h1>
    </header>

    <section class="module-body">
      <!-- Inhalt -->
    </section>
  </main>

  <!-- Shared Scripts ZUERST -->
  <script src="../../shared/dkz-utils.js"></script>
  <script src="../../shared/dkz-navbar.js"></script>
  <script src="../../shared/dkz-debug.js"></script>
  <script src="../../shared/dkz-guide.js"></script>

  <!-- Modul Script ZULETZT -->
  <script src="script.js"></script>
</body>
</html>
```

### Meta Tags (Pflicht)

| Tag | Zweck | Beispiel |
|:----|:------|:---------|
| `charset` | Zeichensatz | `UTF-8` |
| `viewport` | Responsive | `width=device-width, initial-scale=1.0` |
| `description` | SEO/Uebersicht | Kurzbeschreibung des Moduls |
| `theme-color` | Browser-Farbe | `#fa1e4e` |

### Script Loading

- Shared Scripts (`../../shared/`) IMMER VOR Modul-Scripts
- Reihenfolge: `dkz-utils.js` → `dkz-navbar.js` → `dkz-debug.js` → `dkz-guide.js`
- Modul-eigenes `script.js` IMMER am Ende
- KEIN `async` bei Shared Scripts (Abhaengigkeiten!)
- `defer` erlaubt fuer unabhaengige Drittanbieter-Scripts

---

## CSS Standards

### Custom Properties (DkZ Design System)

```css
:root {
  /* Primaerfarben — NIEMALS hartcodiert verwenden! */
  --accent: #fa1e4e;
  --bg: #060608;
  --bg-secondary: #0a0a0f;
  --text: #e8e6e3;
  --text-muted: #6b7280;

  /* Statusfarben */
  --green: #00ff88;
  --yellow: #ffb800;
  --red: #ff3b5c;
  --blue: #3b82f6;

  /* Abstufungen */
  --border: rgba(255, 255, 255, 0.06);
  --glass-bg: rgba(255, 255, 255, 0.05);
  --glass-border: rgba(255, 255, 255, 0.08);

  /* Typografie */
  --font-ui: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  --font-code: 'JetBrains Mono', 'Fira Code', monospace;

  /* Spacing */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
  --space-2xl: 48px;

  /* Border Radius */
  --radius-sm: 6px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-full: 9999px;

  /* Transitions */
  --transition-fast: 150ms ease;
  --transition-normal: 300ms ease;
  --transition-slow: 500ms ease;
}
```

### Glassmorphism (Standard-Stil)

```css
.glass {
  background: var(--glass-bg);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid var(--glass-border);
  border-radius: var(--radius-lg);
}
```

### Responsive Breakpoints

```css
/* Mobile First */
/* Smartphones */
@media (min-width: 480px) { /* ... */ }

/* Tablets */
@media (min-width: 768px) { /* ... */ }

/* Desktop */
@media (min-width: 1024px) { /* ... */ }

/* Widescreen */
@media (min-width: 1440px) { /* ... */ }

/* Ultra-Wide */
@media (min-width: 1920px) { /* ... */ }
```

### Benennungs-Konventionen

```css
/* BEM-artig, aber vereinfacht */
.module-header { }
.module-header__title { }
.module-header--compact { }

/* Status-Klassen */
.is-active { }
.is-loading { }
.is-error { }
.is-hidden { }

/* Utility-Klassen */
.text-center { text-align: center; }
.text-muted { color: var(--text-muted); }
.flex-center { display: flex; align-items: center; justify-content: center; }
```

---

## JavaScript Standards

### esc() Funktion (PFLICHT)

```javascript
/**
 * XSS-sichere Escape-Funktion
 * MUSS bei JEDEM innerHTML mit User-Input verwendet werden
 * Regel: §R1 — Eiserne Regel #1
 */
function esc(str) {
  if (str === null || str === undefined) return '';
  const div = document.createElement('div');
  div.appendChild(document.createTextNode(String(str)));
  return div.innerHTML;
}

// RICHTIG:
container.innerHTML = `<p>${esc(userData)}</p>`;

// FALSCH — VERBOTEN:
// container.innerHTML = `<p>${userData}</p>`;
```

### Event Handling

```javascript
// Event Delegation (bevorzugt)
document.getElementById('list').addEventListener('click', (e) => {
  const item = e.target.closest('[data-action]');
  if (!item) return;

  const action = item.dataset.action;
  const id = item.dataset.id;

  switch (action) {
    case 'edit': handleEdit(id); break;
    case 'delete': handleDelete(id); break;
  }
});

// DOM Ready
document.addEventListener('DOMContentLoaded', () => {
  initModule();
});

// Kein inline onclick — VERBOTEN:
// <button onclick="doSomething()">  ← NEIN
// Stattdessen: addEventListener oder data-action
```

### localStorage API (DkZ Wrapper)

```javascript
// Setzen
DkzStore.set('theme', 'dark');
DkzStore.set('user-settings', { lang: 'de', contrast: 'normal' });

// Lesen
const theme = DkzStore.get('theme', 'dark'); // mit Fallback
const settings = DkzStore.get('user-settings', {});

// Alter pruefen (fuer Cache-Invalidierung)
if (DkzStore.getAge('api-data') > 5 * 60 * 1000) {
  // Aelter als 5 Minuten — neu laden
}

// Loeschen
DkzStore.remove('temp-data');
DkzStore.clear('cache_'); // Alle mit Prefix
```

### Variablen und Funktionen

```javascript
// camelCase fuer Variablen und Funktionen
const moduleConfig = {};
function loadModuleData() { }

// PascalCase fuer Klassen
class DkzModule { }

// UPPER_SNAKE fuer Konstanten
const MAX_RETRIES = 3;
const API_BASE_URL = '/api/v1';

// Kein var — nur const und let
const immutable = 'fest';
let mutable = 'aenderbar';
```

---

## Git Standards

### Commit Message Format

```
<type>(<scope>): <beschreibung>

[optionaler body]

[optionaler footer]
```

### Types

| Type | Verwendung |
|:-----|:-----------|
| `feat` | Neues Feature |
| `fix` | Bugfix |
| `docs` | Nur Dokumentation |
| `style` | Formatierung (kein Code-Change) |
| `refactor` | Code-Umstrukturierung |
| `perf` | Performance-Verbesserung |
| `test` | Tests hinzufuegen/aendern |
| `chore` | Build, CI, Dependencies |

### Beispiele

```bash
feat(dashboard): Ampel-Widget hinzugefuegt
fix(navbar): Aktiver Link wird jetzt korrekt hervorgehoben
docs(wiki): PATTERNS.md erstellt
refactor(copilot): NanoBot Kommunikation vereinfacht
chore(ci): GitHub Actions Workflow aktualisiert
```

### Branch Naming

```
feature/modul-name-kurzbeschreibung
fix/issue-nummer-kurzbeschreibung
docs/was-dokumentiert-wird
refactor/bereich-was-geaendert
release/v2.1.0
```

### Regeln

- Commits auf Deutsch
- Beschreibung max. 72 Zeichen
- Body bei komplexen Aenderungen
- Ein Commit pro logische Aenderung
- IMMER committen nach Abschluss einer Aufgabe

---

## Datei-Standards

### Naming Conventions

| Typ | Convention | Beispiel |
|:----|:-----------|:---------|
| Module | `lowercase-bindestrich/` | `system-check/` |
| Shared JS | `dkz-[funktion].js` | `dkz-navbar.js` |
| CSS | `style.css` (Modul) | `modules/xyz/style.css` |
| Config | `[name].json` | `features.json` |
| Docs | `UPPERCASE.md` | `README.md`, `PATTERNS.md` |
| Workflows | `[name].yml` | `deploy.yml` |

### Datei-Header (empfohlen)

```javascript
/**
 * DEVKiTZ — Modul Name
 * @description Kurze Beschreibung
 * @version 2.0.0
 * @date 2026-05-30
 * @module modul-ordner-name
 */
```

---

## Verbotene Praktiken

| Verboten | Stattdessen |
|:---------|:------------|
| `#fa1e4e` hartcodiert | `var(--accent)` |
| `console.log` in Produktion | `DkzDebug.log()` |
| `innerHTML` ohne `esc()` | `esc(userInput)` |
| jQuery | Vanilla JS |
| React/Vue/Angular | Vanilla HTML+CSS+JS |
| `var` | `const` oder `let` |
| Inline `onclick` | `addEventListener` |
| Nackte URLs in Docs | `[Text](url)` |

---

*Coding Standards v1.0 · DEVKiTZ Ecosystem*
