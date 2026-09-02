# signin-scan-animation

A small "device verification" animation for **Sign in** screens: a laptop sits
inside a viewfinder while an accent‑coloured scan line sweeps down it, lights the
drawing and the fingerprint chip, rests, and sweeps back.

Pure **CSS + inline SVG**. No JavaScript needed, no image files, no
dependencies. Works on a dark or a light card.

```
 ┌───────────────┐        line sweeps down  (~0.8s)
 │  ▁▁▁▁▁▁▁▁▁▁▁  │  ◉     rests at the bottom (~1.5s)
 │  █ laptop  █  │        sweeps back up      (~1.1s)
 └───────────────┘        loops (3.5s total)
```

## Files

| File | What it is |
| --- | --- |
| `signin-scan.css` | The stylesheet — the animation and all layout. |
| `signin-scan.html` | The markup block to paste next to your form (needs the CSS). |
| `signin-scan.js` | Optional `<signin-scan>` web component (styles + SVG bundled, shadow DOM). |
| `index.html` | Self‑contained landing page: live demo, embed snippets, and the variable table. |

**Live:** <https://ogabek-karimov.github.io/signin-scan-animation/>

`index.html` needs nothing else — open the file directly, or serve the folder
with `npx serve .`.

## Use it

### Option A — CSS + HTML (simplest)

```html
<link rel="stylesheet" href="signin-scan.css" />

<!-- drop this where you want the graphic; one instance per page -->
<!-- ...contents of signin-scan.html... -->
<div class="ssa" role="img" aria-label="Verifying this device"> … </div>
```

Add `ssa--light` for a light background: `<div class="ssa ssa--light">`.

### Option B — Web component

```html
<script src="signin-scan.js" type="module"></script>

<signin-scan></signin-scan>
<signin-scan light></signin-scan>
<signin-scan style="--ssa-zoom: 1.4"></signin-scan>
```

Styles and SVG live in a shadow root, so you can place several on one page and
it will not touch the rest of your CSS.

### Option C — iframe

Host `index.html` (or a trimmed copy with just the widget) and embed it:

```html
<iframe src="signin-scan/index.html" width="160" height="120" style="border:0"
        title="Verifying this device"></iframe>
```

## Theming

Override these on `.ssa` (Option A) or the `<signin-scan>` element (Option B):

| Variable | Default (dark) | Purpose |
| --- | --- | --- |
| `--ssa-accent` | `#2a77d7` | Scan line, glow, "scanned" laptop and chip. |
| `--ssa-body-fill` | `#242427` | Laptop shell / chip background. |
| `--ssa-body-stroke` | `#5b5a5c` | Laptop outline before the line passes. |
| `--ssa-screen-fill` | `#212123` | Laptop screen fill before the line passes. |
| `--ssa-chip-ring-idle` | `#4a4a4d` | Fingerprint chip ring, idle. |
| `--ssa-glyph-idle` | `#6b6b6e` | Fingerprint glyph, idle. |
| `--ssa-duration` | `3.5s` | One full sweep‑down / rest / sweep‑up. |
| `--ssa-zoom` | `1` | Scales the whole widget (base size 157 × 119). |

The `ssa--light` class / `light` attribute just re‑sets the greys for a light card.

Example — brand colour and larger:

```css
.ssa { --ssa-accent: #6d5efc; --ssa-zoom: 1.5; }
```

## Accessibility

- The graphic is decorative; wrappers carry `role="img"` + an `aria-label` and
  the inner SVGs are `aria-hidden`.
- `prefers-reduced-motion: reduce` stops the loop and shows the calm idle state.

## Browser support

Needs `@property` (for the smooth scan interpolation) and `color-mix()` — Chrome/
Edge 111+, Safari 16.4+, Firefox 128+. Older browsers still render the laptop and
a stepped animation; an `rgba()` fallback covers the tinted border and glow.

## Credit

Rebuilt from the markup of a device‑verification sign‑in dialog and a screen
recording of its motion, then reorganised into a standalone, themeable component.

## License

MIT — see [LICENSE](LICENSE).
