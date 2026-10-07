# Fonts

Use `next/font` (self-hosted, no layout shift, no third-party request at runtime). The font is exposed as a CSS variable that the project's font-family tokens (`--font-family-primary`, `--font-family-secondary`) consume. Font family is a per-project value.

```js
// documentation snippet: lib/config/fonts.js
import { Inter } from "next/font/google";
export const fontPrimary = Inter({ subsets: ["latin"], display: "swap", variable: "--font-primary" });
```

```jsx
// documentation snippet: app/layout.js
<html lang="en" className={fontPrimary.variable}>
```

## Rules

- **Prefer one family**, ideally a variable font (one file covers all weights). A second family needs a clear brand reason.
- Never load `100..900` blanket. Static fonts: only the weights used (typically 400, 500/600, 700).
- `subsets: ["latin"]`; add others only if content needs them.
- `display: "swap"`; `next/font` generates size-adjusted fallback metrics so swapping causes ~no CLS.
- `preload` only fonts used above the fold; secondary/mono fonts `preload: false`.
- Local brand fonts: `next/font/local` with `woff2` only.
- No icon fonts; use inline SVG with per-icon imports.
- Budget: <= 2 font files, <= 100KB each (woff2).
- Debug: DevTools Network -> Font; confirm files load from your origin; confirm LCP text isn't blocked on the font; confirm no CLS on swap.
