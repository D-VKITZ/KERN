---
description: Batch fix all modules for DkZ compliance
---

# Batch Module Fix

Scanne ALLE Module in `01_PROJECTS/01_dashboard/modules/` und fixe sie.

## Fuer JEDES Modul:

1. **Pruefe** ob index.html existiert â†’ wenn nicht, ueberspringe
2. **XSS Check**: `innerHTML` ohne `esc()` â†’ Fix mit esc()
3. **CSS Variables**: Hardcoded HEX â†’ `var(--accent)` etc.
4. **Shared Scripts**: Fehlende Scripts am Body-Ende â†’ hinzufuegen
5. **Meta Tags**: `dkz-version` fehlt â†’ hinzufuegen
6. **Hub Button**: Fehlt â†’ hinzufuegen

## Batch-Strategie

- Maximal 10 Module pro PR
- Commit pro Modul: `fix({moduleName}): DkZ Compliance`
- PR Titel: `fix: DkZ Compliance Batch {N} ({count} Module)`
- PR Body: Tabelle mit allen Modulen und gefundenen Problemen
- Label: `ðŸ¤– copilot`, `ðŸ”§ fix`, `ðŸ“± handy`
- Reviewer: @7IKED

## Prioritaet

1. Module mit XSS-Luecken zuerst (ðŸ”´)
2. Module ohne Shared Scripts (ðŸŸ¡)
3. Module ohne Meta Tags (ðŸŸ¢)
