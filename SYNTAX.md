# DEVKiTZ Coding Standards

## HTML Standards
- DOCTYPE: html5
- Meta: charset UTF-8, viewport, dkz-version
- Fonts: Google Fonts Inter + JetBrains Mono
- Scripts: defer, am Ende von body
- Hub Link: ../../hub/index.html

## CSS Standards
- Custom Properties: --bg, --green, --accent, --text
- Font: var(--font) Inter, var(--mono) JetBrains
- Glassmorphism: backdrop-filter blur 20px
- Border: rgba 255,255,255,0.06
- Animation: fadeUp 0.3s ease

## JS Standards
- esc() bei JEDEM innerHTML
- Kein console.log in Produktion
- localStorage fuer Persistenz
- Event Delegation wo moeglich
- const/let statt var

## Git Standards
- Commit: feat(bereich): beschreibung
- Branch: feature/name oder fix/name
- Push: Nach JEDER Aenderung
- Tag: v1.00.0_01 Format