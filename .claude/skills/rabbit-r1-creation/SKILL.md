---
name: rabbit-r1-creation
description: Build apps for the rabbit r1 (240×282 portrait display, scrollwheel + push-to-talk button). Defines the BRAUN / Dieter-Rams "Papier" design system that is the house style for ALL of this user's UI work — r1 Creations, web apps, dashboards, anything device-like or focused on a single task. Trigger whenever building, redesigning, or styling a user interface; whenever creating HTML/CSS for an r1 Creation; whenever the user mentions "r1", "Creation", "BRAUN", "Rams", "Papier", or asks for a design refresh.
---

# r1 Creations · BRAUN Design System

The house style for **every UI** the user builds. Inspired by Dieter Rams and the BRAUN formal language of the 1970s–80s. Reference assets live alongside this file in `assets/`.

> **Leitsatz — Weniger, aber besser.**

---

## 0 · Quick reference (copy-paste tokens)

```css
:root {
  /* Type */
  --mono:    'IBM Plex Mono', ui-monospace, 'SF Mono', monospace;
  --sans:    'Helvetica Neue', Helvetica, -apple-system, Arial, sans-serif;

  /* Papier (the chosen variant — bright, calm, daylight) */
  --beton:   #D7D4CC;   /* page background */
  --paper:   #E7E4DE;   /* display / canvas */
  --surface: #F0EEE9;   /* input surfaces, raised cells */
  --ink:     #1B1A17;   /* text */
  --muted:   #8A867E;   /* secondary text, mono labels */
  --line:    #C7C3BA;   /* hairlines, dividers */
  --accent:  #D75A1E;   /* BRAUN orange — active element only */
  --acf:     #FFFFFF;   /* foreground on accent */
  --ocker:   #C8862E;   /* tertiary, used sparingly */
}
```

Load fonts:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">
```

---

## 1 · Principles (Rams, applied)

| # | Principle | What it means here |
|---|-----------|--------------------|
| 01 | **Macht ein Produkt brauchbar** | One Creation, one task. The first screen IS the function — no menu, no settings dance. |
| 02 | **Ist ehrlich** | Values shown as they are. Monospaced, precise, no decoration. Nothing pretends to be what it isn't. |
| 03 | **Ist verständlich** | Wheel scrolls, button confirms. Two inputs, behaving the same everywhere. |
| 04 | **Ist unaufdringlich** | Neutral surfaces, ONE accent color. The display is a tool, not a stage. |
| 05 | **Ist konsequent bis ins Detail** | One grid, one type system, one motion language. Nothing left to chance. |
| 06 | **Ist so wenig Design wie möglich** | When in doubt, remove it. What remains carries a function. |

If a UI choice violates one of these, do it differently.

---

## 2 · Display & grid

| Token | Value |
|-------|-------|
| Device canvas | **240 × 282 px**, portrait |
| Base grid | **4 px** — every dimension is a multiple |
| Screen margin | **16 px** all sides |
| Header band | 40 px |
| Action band | 48 px (bottom) |

**Spacing scale (px):** `4 · 8 · 12 · 16 · 24 · 32`
- 4 — hairline gap
- 8 — icon ↔ text
- 12 — list line spacing
- 16 — screen edge
- 24 — block separation
- 32 — section separation

**Radii (px):** `0` sharp · `2` controls/buttons · `6` screen container · `9999` knobs only.

---

## 3 · Color

**The Papier variant is the chosen one.** Anthrazit and Signal exist but were rejected — do not use them unless the user explicitly asks for a dark theme.

| Name | Hex | Use |
|------|-----|-----|
| Papier | `#EDEBE6` / `#E7E4DE` | Display canvas |
| Beton | `#D7D4CC` | Page around the device |
| Surface | `#F0EEE9` | Inputs, raised cells, keypad keys |
| Grau (Muted) | `#8A867E` | Secondary text, mono labels |
| Line | `#C7C3BA` | Dividers, scrollbar track |
| Tinte (Ink) | `#1B1A17` | Primary text |
| **Akzent** | **`#D75A1E`** | BRAUN orange |
| Ocker | `#C8862E` | Tertiary signal, used rarely |

**Accent rule — strictly enforced:**
- Exactly **one** active element per screen carries the accent.
- Never as a decorative surface. Never as branding.
- Use it for: the current selection, the primary action button, an active progress bar, a live indicator. That's it.

### Dark variants (only when asked)

```css
/* Anthrazit — device-like, dimmed */
--bg:#232220; --sf:#2E2C29; --fg:#ECEAE4; --mut:#8F8B83; --line:#403E39; --accent:#E2641F; --acf:#171108;

/* Signal — accent dominates (high-contrast, alarm-like) */
--bg:#161513; --sf:#201F1B; --fg:#F2F0EA; --mut:#9A958C; --line:#34322D; --accent:#F26A1B; --acf:#161513;
```

---

## 4 · Typography

**Two faces, two jobs:**
- **Helvetica Neue** → speaks. Titles, labels, body. Weights 400 / 500 / 700.
- **IBM Plex Mono** → measures. Times, numbers, frequencies, technical labels. Tabular figures.

| Role | Size / weight | Notes |
|------|---------------|-------|
| Display | 42 / 700 | letter-spacing −2% |
| Title | 28 / 700 | −1% |
| Body | 17 / 500 | hints, sentences |
| Secondary | 14 / 400 | mut color |
| Mono label | 11 mono / 500 | **UPPERCASE**, letter-spacing +12% |

On the 240-px display, scale these down (mono label often 10 px, display often 32–46 px). Keep the ratios.

---

## 5 · Iconography

Pure geometry — **circle, line, triangle, square**. SVG only.

- Stroke: **2 px**
- Grid: **24 × 24** viewBox (sometimes 26)
- `stroke="currentColor"` so they inherit ink/accent
- No fill detail, no shadows, no gradients
- Names stay lowercase, monospaced when labelled (e.g. `power`, `play`, `mic · ptt`)

```html
<!-- timer -->
<svg width="26" height="26" viewBox="0 0 26 26" fill="none" stroke="currentColor" stroke-width="2">
  <circle cx="13" cy="13" r="8"/><path d="M13 8 V13 L17 15"/>
</svg>
```

---

## 6 · Components

### Buttons
```html
<button class="btn primary">Bestätigen</button>           <!-- accent fill -->
<button class="btn secondary">Abbrechen</button>          <!-- 1px ink outline -->
<button class="btn text">Mehr</button>                    <!-- underlined, mut -->
```
```css
.btn { font: 700 13px var(--sans); padding: 12px; border-radius: 2px; border: none; cursor: pointer; }
.btn.primary   { background: var(--accent); color: var(--acf); }
.btn.secondary { background: transparent; color: var(--ink); border: 1px solid var(--ink); font-weight: 500; }
.btn.text      { background: none; color: var(--muted); text-decoration: underline; text-underline-offset: 3px; }
.btn:active    { opacity: .7; }
```

### List row (the canonical r1 navigation pattern)
The wheel moves selection — the **selected row carries the accent**, everything else is neutral. Button opens.
```html
<div class="row active">Timer <span class="chev">▸</span></div>
<div class="row">Rechner <span class="chev">▸</span></div>
```
```css
.row { display:flex; justify-content:space-between; padding:13px 14px; font:500 15px var(--sans); border-bottom:1px solid var(--line); }
.row.active { background: var(--accent); color: var(--acf); border-bottom: none; border-radius: 2px; }
.chev { font-family: var(--mono); font-size: 12px; color: var(--muted); }
.row.active .chev { color: var(--acf); opacity: .85; }
```

### Toggle / Stepper / Slider / Segmented
Borders are 1 px ink. Filled track + thumb use accent. Off-state uses `--line`.

### Display values
Always mono, tabular:
```html
<div class="value">02:48<span class="cs">.39</span></div>
```
```css
.value { font: 500 46px var(--mono); letter-spacing: -2%; }
.value .cs { font-size: 18px; color: var(--muted); }
```

---

## 7 · Motion

| Token | Duration | Use |
|-------|----------|-----|
| `tap / detent` | **120 ms** | Immediate feedback (button press, wheel click) |
| `transition` | **200 ms** | Screen ↔ screen |
| `fade-in` | **320 ms** | Content appears |

Easings:
- Standard: `cubic-bezier(.4, 0, .2, 1)` — calm, no overshoot
- Entrance: `cubic-bezier(.2, .7, .2, 1)` — soft landing

**Never bounce. Never overshoot.** Motion shows only what actually changes.

---

## 8 · Interaction — the two-input rule

Every Creation is operable with **scrollwheel + push-to-talk button** and nothing else.

- **Scrollwheel** → navigates lists, adjusts values, pages between screens. Each detent = one step. The selected element carries the accent.
- **Button** → always the primary action of the current screen. Hold = speak. Tap = confirm.

On the web (development), map:
- `↑` / `↓` or `wheel` → scrollwheel
- `Space` (hold) → push-to-talk
- `Enter` → button tap

Document these in a small mono-styled help text below the device frame.

---

## 9 · Starter template

A self-contained r1 Creation skeleton — copy and replace the body.

```html
<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<title>Creation</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{
  --mono:'IBM Plex Mono',ui-monospace,'SF Mono',monospace;
  --beton:#D7D4CC;--paper:#E7E4DE;--surface:#F0EEE9;
  --ink:#1B1A17;--muted:#8A867E;--line:#C7C3BA;
  --accent:#D75A1E;--acf:#FFFFFF;
}
::selection{background:var(--accent);color:#fff}
html,body{width:100%;min-height:100vh;background:var(--beton);color:var(--ink);
  font-family:'Helvetica Neue',Helvetica,-apple-system,Arial,sans-serif;
  -webkit-font-smoothing:antialiased;-webkit-user-select:none;user-select:none}
body{display:flex;flex-direction:column;align-items:center;justify-content:center;padding:20px}
#device{width:240px;height:282px;background:var(--paper);color:var(--ink);
  display:flex;flex-direction:column;position:relative;overflow:hidden;
  border-radius:6px;border:1px solid rgba(0,0,0,.18);
  box-shadow:0 2px 0 rgba(0,0,0,.06),0 16px 44px rgba(27,26,23,.18)}
#header{padding:7px 12px 6px;display:flex;align-items:center;justify-content:space-between;
  border-bottom:1px solid var(--line);flex-shrink:0;
  font-family:var(--mono);font-size:11px;font-weight:600;color:var(--accent);
  letter-spacing:1.5px;text-transform:uppercase}
#help{margin-top:18px;max-width:320px;font-family:var(--mono);font-size:10px;
  letter-spacing:.02em;color:var(--muted);line-height:1.7;text-align:center}
#help b{color:var(--accent);font-weight:600}
#help kbd{display:inline-block;padding:1px 6px;border-radius:2px;
  background:#E9E6E0;border:1px solid var(--line);
  font-family:var(--mono);font-size:10px;color:var(--ink)}
</style>
</head>
<body>
  <div id="device">
    <div id="header"><span>Creation</span><span></span></div>
    <!-- content -->
  </div>
  <div id="help">
    <kbd>Space</kbd> halten = Sprache &nbsp;·&nbsp;
    <kbd>Enter</kbd> = Bestätigen &nbsp;·&nbsp;
    <kbd>↑</kbd>/<kbd>↓</kbd> = scrollen
  </div>
  <script>
    // wheel → selection, space → primary action
  </script>
</body>
</html>
```

---

## 10 · Checklist before shipping

- [ ] First screen shows the function — no menu in front of it
- [ ] Exactly one accent element visible at a time
- [ ] Wheel and button alone can drive everything
- [ ] All values that *measure* are in IBM Plex Mono with tabular figures
- [ ] All spacing is a multiple of 4
- [ ] Nothing decorative — every element earns its place
- [ ] Motion stays under 320 ms; nothing bounces
- [ ] Help text below the device explains the two inputs

If a box stays unchecked, fix it or remove what's in the way.

---

## Assets

- `assets/design-system.html` — the full visual reference (open in a browser)
- `assets/anthrazit.png` — reference screenshot of the rejected dark variant (for comparison only)

When in doubt about a visual decision, open the reference HTML and match it.
