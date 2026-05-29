# DkZ Design Patterns

> Stand: 2026-05-30 · Zentrale Pattern-Bibliothek fuer das DEVKiTZ Oekosystem
> Jedes Pattern mit Code-Beispiel und Einsatzbereich

---

## UI Patterns

### Glassmorphism Card

Halbtransparente Karten mit Blur-Effekt — Kerndesign-Element aller Module.

```css
.glass-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 16px;
  padding: 24px;
  transition: all 0.3s ease;
}

.glass-card:hover {
  background: rgba(255, 255, 255, 0.08);
  border-color: var(--accent);
  box-shadow: 0 0 30px rgba(250, 30, 78, 0.15);
}
```

**Einsatz:** Modul-Container, Info-Panels, Dashboard-Widgets

---

### Neon Glow

Leuchtende Akzente fuer aktive Elemente und CTAs.

```css
.neon-glow {
  box-shadow:
    0 0 5px var(--accent),
    0 0 15px rgba(250, 30, 78, 0.3),
    0 0 30px rgba(250, 30, 78, 0.1);
  border: 1px solid var(--accent);
}

.neon-text {
  color: var(--green);
  text-shadow:
    0 0 5px var(--green),
    0 0 15px rgba(0, 255, 136, 0.3);
}

/* Pulsierender Glow */
@keyframes pulse-glow {
  0%, 100% { box-shadow: 0 0 5px var(--accent); }
  50% { box-shadow: 0 0 20px var(--accent), 0 0 40px rgba(250, 30, 78, 0.2); }
}
```

**Einsatz:** Buttons, Status-Indikatoren, aktive Navigation

---

### Split Layout

Zweispalten-Layout mit fester Sidebar und scrollbarem Content.

```css
.split-layout {
  display: grid;
  grid-template-columns: 280px 1fr;
  height: 100vh;
  overflow: hidden;
}

.split-sidebar {
  background: rgba(6, 6, 8, 0.95);
  border-right: 1px solid rgba(255, 255, 255, 0.06);
  overflow-y: auto;
  padding: 20px;
}

.split-content {
  overflow-y: auto;
  padding: 32px;
  scroll-behavior: smooth;
}

@media (max-width: 768px) {
  .split-layout {
    grid-template-columns: 1fr;
  }
  .split-sidebar {
    display: none;
  }
}
```

**Einsatz:** Einstellungen, Dokumentation, File-Browser

---

### Sidebar + Content

Navbar-integriertes Layout mit collapsible Sidebar.

```html
<div class="app-layout">
  <nav class="dkz-navbar" id="navbar"></nav>
  <aside class="sidebar" id="sidebar">
    <div class="sidebar-header">
      <h3>Navigation</h3>
      <button class="sidebar-toggle" onclick="toggleSidebar()">
        &#9776;
      </button>
    </div>
    <ul class="sidebar-nav">
      <li><a href="#section1" class="active">Uebersicht</a></li>
      <li><a href="#section2">Details</a></li>
    </ul>
  </aside>
  <main class="main-content" id="content">
    <!-- Module Content -->
  </main>
</div>
```

```javascript
function toggleSidebar() {
  const sidebar = document.getElementById('sidebar');
  sidebar.classList.toggle('collapsed');
  localStorage.setItem('sidebar-state',
    sidebar.classList.contains('collapsed') ? 'collapsed' : 'expanded'
  );
}
```

**Einsatz:** Dashboard-Module, Admin-Panels

---

## Data Patterns

### localStorage Pattern

Typsicherer localStorage Wrapper mit Fallback und Versionierung.

```javascript
const DkzStore = {
  VERSION: '2.0',

  set(key, value) {
    try {
      const data = {
        value,
        timestamp: Date.now(),
        version: this.VERSION
      };
      localStorage.setItem(`dkz_${key}`, JSON.stringify(data));
      return true;
    } catch (e) {
      console.error(`[DkzStore] Speicherfehler: ${e.message}`);
      return false;
    }
  },

  get(key, fallback = null) {
    try {
      const raw = localStorage.getItem(`dkz_${key}`);
      if (!raw) return fallback;
      const data = JSON.parse(raw);
      return data.value !== undefined ? data.value : fallback;
    } catch {
      return fallback;
    }
  },

  remove(key) {
    localStorage.removeItem(`dkz_${key}`);
  },

  clear(prefix = 'dkz_') {
    Object.keys(localStorage)
      .filter(k => k.startsWith(prefix))
      .forEach(k => localStorage.removeItem(k));
  },

  getAge(key) {
    try {
      const raw = localStorage.getItem(`dkz_${key}`);
      if (!raw) return Infinity;
      const data = JSON.parse(raw);
      return Date.now() - (data.timestamp || 0);
    } catch {
      return Infinity;
    }
  }
};
```

**Einsatz:** Offline-First Datenspeicherung, Settings, Cache

---

### IndexedDB Wrapper

Asynchroner IndexedDB Wrapper fuer groessere Datenmengen.

```javascript
class DkzDB {
  constructor(dbName = 'devkitz', version = 1) {
    this.dbName = dbName;
    this.version = version;
    this.db = null;
  }

  async open(stores = ['modules', 'settings', 'cache']) {
    return new Promise((resolve, reject) => {
      const request = indexedDB.open(this.dbName, this.version);
      request.onupgradeneeded = (e) => {
        const db = e.target.result;
        stores.forEach(name => {
          if (!db.objectStoreNames.contains(name)) {
            db.createObjectStore(name, { keyPath: 'id' });
          }
        });
      };
      request.onsuccess = (e) => {
        this.db = e.target.result;
        resolve(this.db);
      };
      request.onerror = (e) => reject(e.target.error);
    });
  }

  async put(store, data) {
    return new Promise((resolve, reject) => {
      const tx = this.db.transaction(store, 'readwrite');
      tx.objectStore(store).put({ ...data, updatedAt: Date.now() });
      tx.oncomplete = () => resolve(true);
      tx.onerror = (e) => reject(e.target.error);
    });
  }

  async get(store, id) {
    return new Promise((resolve, reject) => {
      const tx = this.db.transaction(store, 'readonly');
      const request = tx.objectStore(store).get(id);
      request.onsuccess = () => resolve(request.result || null);
      request.onerror = (e) => reject(e.target.error);
    });
  }

  async getAll(store) {
    return new Promise((resolve, reject) => {
      const tx = this.db.transaction(store, 'readonly');
      const request = tx.objectStore(store).getAll();
      request.onsuccess = () => resolve(request.result);
      request.onerror = (e) => reject(e.target.error);
    });
  }
}
```

**Einsatz:** Modul-Daten, Offline-Archive, Grosse Datasets

---

### Fetch + Cache

HTTP-Fetch mit Cache-Layer und Retry-Logik.

```javascript
async function dkzFetch(url, options = {}) {
  const {
    cache = true,
    cacheTTL = 5 * 60 * 1000, // 5 Minuten
    retries = 3,
    retryDelay = 1000
  } = options;

  // Cache pruefen
  if (cache) {
    const cacheKey = `fetch_${btoa(url)}`;
    const cached = DkzStore.get(cacheKey);
    if (cached && DkzStore.getAge(cacheKey) < cacheTTL) {
      return cached;
    }
  }

  // Fetch mit Retry
  let lastError;
  for (let i = 0; i < retries; i++) {
    try {
      const response = await fetch(url, {
        headers: { 'Accept': 'application/json' },
        ...options
      });

      if (!response.ok) {
        throw new Error(`HTTP ${response.status}: ${response.statusText}`);
      }

      const data = await response.json();

      // Cache speichern
      if (cache) {
        DkzStore.set(`fetch_${btoa(url)}`, data);
      }

      return data;
    } catch (e) {
      lastError = e;
      if (i < retries - 1) {
        await new Promise(r => setTimeout(r, retryDelay * (i + 1)));
      }
    }
  }

  throw lastError;
}
```

**Einsatz:** API-Calls, GitHub API, externe Datenquellen

---

## Agent Patterns

### Ralph-Loop Pattern

6-Phasen Task-Execution mit frischem Kontext pro Iteration.

```javascript
// Ralph-Loop Executor
const RalphLoop = {
  phases: ['LESEN', 'SPAWN', 'EXECUTE', 'VERIFY', 'COMMIT', 'LOOP'],

  async execute(task) {
    const context = {
      taskId: task.id,
      startTime: Date.now(),
      phase: 0,
      results: []
    };

    // Phase 1: LESEN
    context.phase = 0;
    const spec = await this.loadSpec(task);
    const constitution = await this.loadConstitution();

    // Phase 2: SPAWN — Frischer Kontext
    context.phase = 1;
    const freshContext = this.createFreshContext(spec, constitution);

    // Phase 3: EXECUTE
    context.phase = 2;
    const result = await this.executeTask(freshContext, task);

    // Phase 4: VERIFY
    context.phase = 3;
    const verified = await this.verify(result);
    if (!verified.passed) {
      return { success: false, errors: verified.errors };
    }

    // Phase 5: COMMIT
    context.phase = 4;
    await this.commit(result, task);

    // Phase 6: LOOP — Naechster Task
    context.phase = 5;
    return { success: true, result, duration: Date.now() - context.startTime };
  },

  createFreshContext(spec, constitution) {
    // Kernprinzip: Kein Context Drift
    return {
      rules: constitution.rules,
      task: spec,
      memory: {}, // Frisch!
      timestamp: Date.now()
    };
  }
};
```

**Einsatz:** Automatisierte Task-Ausfuehrung, Agent Workflows

---

### Health-Check Chain

Kaskadierte Gesundheitspruefung aller Systemkomponenten.

```javascript
const HealthChain = {
  checks: [],

  register(name, checkFn, priority = 5) {
    this.checks.push({ name, check: checkFn, priority });
    this.checks.sort((a, b) => a.priority - b.priority);
  },

  async runAll() {
    const results = {
      timestamp: new Date().toISOString(),
      status: 'GREEN', // GREEN, YELLOW, RED
      checks: [],
      duration: 0
    };

    const start = Date.now();

    for (const check of this.checks) {
      try {
        const result = await check.check();
        results.checks.push({
          name: check.name,
          status: result.ok ? 'GREEN' : 'YELLOW',
          message: result.message || 'OK',
          duration: result.duration || 0
        });

        if (!result.ok && results.status === 'GREEN') {
          results.status = 'YELLOW';
        }
      } catch (e) {
        results.checks.push({
          name: check.name,
          status: 'RED',
          message: e.message,
          error: true
        });
        results.status = 'RED';
      }
    }

    results.duration = Date.now() - start;
    return results;
  }
};

// Registrierung
HealthChain.register('localStorage', async () => {
  try {
    localStorage.setItem('_health', '1');
    localStorage.removeItem('_health');
    return { ok: true };
  } catch {
    return { ok: false, message: 'localStorage nicht verfuegbar' };
  }
}, 1);

HealthChain.register('navbar', async () => {
  const nav = document.getElementById('navbar');
  return { ok: !!nav, message: nav ? 'OK' : 'Navbar fehlt' };
}, 2);
```

**Einsatz:** System-Check Modul, Startup-Validierung

---

### NanoBot Communication

Inter-Agent Kommunikation ueber die NanoChat Bridge.

```javascript
class NanoBot {
  constructor(name, port = 3040) {
    this.name = name;
    this.port = port;
    this.ws = null;
    this.handlers = new Map();
  }

  connect() {
    this.ws = new WebSocket(`ws://localhost:${this.port}/nanochat`);

    this.ws.onmessage = (event) => {
      const msg = JSON.parse(event.data);
      const handler = this.handlers.get(msg.type);
      if (handler) handler(msg);
    };

    this.ws.onclose = () => {
      setTimeout(() => this.connect(), 3000); // Auto-Reconnect
    };
  }

  send(type, payload) {
    if (this.ws?.readyState === WebSocket.OPEN) {
      this.ws.send(JSON.stringify({
        from: this.name,
        type,
        payload,
        timestamp: Date.now()
      }));
    }
  }

  on(type, handler) {
    this.handlers.set(type, handler);
  }
}

// Beispiel
const bot = new NanoBot('antigravity');
bot.connect();
bot.on('task', (msg) => {
  // Task empfangen und ausfuehren
});
bot.send('status', { state: 'ready' });
```

**Einsatz:** Agent-zu-Agent Kommunikation, Dashboard-Updates

---

## Code Patterns

### esc() XSS Protection

PFLICHT bei jedem innerHTML mit User-Input.

```javascript
function esc(str) {
  if (str === null || str === undefined) return '';
  const div = document.createElement('div');
  div.appendChild(document.createTextNode(String(str)));
  return div.innerHTML;
}

// Verwendung — RICHTIG:
element.innerHTML = `<span>${esc(userInput)}</span>`;

// FALSCH — NIEMALS:
// element.innerHTML = `<span>${userInput}</span>`;

// Auch in Template Literals:
const html = `
  <div class="card">
    <h3>${esc(title)}</h3>
    <p>${esc(description)}</p>
    <span class="tag">${esc(category)}</span>
  </div>
`;
```

**Einsatz:** UEBERALL wo User-Input in DOM eingefuegt wird

---

### i18n Toggle

Sprachumschaltung mit localStorage-Persistenz.

```javascript
const i18n = {
  current: localStorage.getItem('dkz_lang') || 'de',
  translations: {
    de: {
      dashboard: 'Dashboard',
      settings: 'Einstellungen',
      save: 'Speichern',
      cancel: 'Abbrechen'
    },
    en: {
      dashboard: 'Dashboard',
      settings: 'Settings',
      save: 'Save',
      cancel: 'Cancel'
    }
  },

  t(key) {
    return this.translations[this.current]?.[key] || key;
  },

  setLang(lang) {
    this.current = lang;
    localStorage.setItem('dkz_lang', lang);
    document.querySelectorAll('[data-i18n]').forEach(el => {
      el.textContent = this.t(el.dataset.i18n);
    });
  }
};
```

**Einsatz:** Mehrsprachige Module, UI-Lokalisierung

---

### Contrast Mode

Barrierefreie Kontrastumschaltung.

```javascript
function toggleContrast() {
  const body = document.body;
  const isHigh = body.classList.toggle('high-contrast');
  localStorage.setItem('dkz_contrast', isHigh ? 'high' : 'normal');
}

// CSS
/* .high-contrast {
  --bg: #000000;
  --text: #ffffff;
  --accent: #ff4444;
  --border: rgba(255, 255, 255, 0.3);
} */

// Beim Laden wiederherstellen
if (localStorage.getItem('dkz_contrast') === 'high') {
  document.body.classList.add('high-contrast');
}
```

**Einsatz:** Barrierefreiheit, Accessibility

---

### PWA Setup

Progressive Web App Grundgeruest.

```javascript
// Service Worker Registrierung
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js')
    .then(reg => {
      // Update Check
      reg.addEventListener('updatefound', () => {
        const worker = reg.installing;
        worker.addEventListener('statechange', () => {
          if (worker.state === 'activated') {
            // Neue Version verfuegbar
          }
        });
      });
    });
}

// Manifest (manifest.json)
// {
//   "name": "DEVKiTZ Dashboard",
//   "short_name": "DkZ",
//   "start_url": "/",
//   "display": "standalone",
//   "background_color": "#060608",
//   "theme_color": "#fa1e4e",
//   "icons": [
//     { "src": "/icons/icon-192.png", "sizes": "192x192", "type": "image/png" },
//     { "src": "/icons/icon-512.png", "sizes": "512x512", "type": "image/png" }
//   ]
// }
```

**Einsatz:** Offline-Faehigkeit, Mobile Installation

---

*Pattern Library v1.0 · DEVKiTZ Design System*
