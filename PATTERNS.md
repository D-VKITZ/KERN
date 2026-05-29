# DEVKiTZ Design Patterns

## UI Pattern: Glassmorphism Card

```css
.glass-card {
  background: rgba(255,255,255,0.03);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255,255,255,0.06);
  border-radius: 12px;
  padding: 16px;
}
```

## UI Pattern: Neon Glow

```css
.neon-glow {
  text-shadow: 0 0 20px rgba(0,255,136,0.3), 0 0 60px rgba(0,255,136,0.1);
  color: var(--green);
}
```

## Data Pattern: localStorage Wrapper

```javascript
const Store = {
  get(key, fallback=[]) {
    try { return JSON.parse(localStorage.getItem(key)) || fallback }
    catch { return fallback }
  },
  set(key, val) { localStorage.setItem(key, JSON.stringify(val)) },
  remove(key) { localStorage.removeItem(key) }
};
```

## Security Pattern: XSS Protection

```javascript
function esc(s) {
  const d = document.createElement('div');
  d.textContent = String(s);
  return d.innerHTML;
}
// IMMER: element.innerHTML = esc(userInput)
```

## Agent Pattern: Ralph-Loop

```
1. LESEN: prd.json + constitution
2. SPAWN: Frischer Kontext
3. EXECUTE: Code schreiben
4. VERIFY: Tests + Review
5. COMMIT: Git + prd.json update
6. LOOP: Naechster Task
```

## i18n Pattern: EN/DE Toggle

```javascript
const i18n = {
  en: { title: 'Dashboard', save: 'Save' },
  de: { title: 'Dashboard', save: 'Speichern' }
};
let lang = 'en';
function t(key) { return i18n[lang][key] || key; }
```

## PWA Pattern: Manifest

```json
{
  "name": "DkZ Module",
  "short_name": "DkZ",
  "start_url": ".",
  "display": "standalone",
  "background_color": "#000000",
  "theme_color": "#00ff88"
}
```