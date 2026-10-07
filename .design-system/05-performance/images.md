# Images

Every image is evaluated for: dimensions, file size, format, compression, responsive sizing, lazy/priority, aspect ratio, alt text.

```jsx
// documentation snippet
// Above the fold, the ONE likely-LCP image
<Image src={hero} alt="Descriptive alt" width={1200} height={800} priority sizes="(min-width: 1024px) 50vw, 100vw" />

// Below the fold: default lazy loading, sized to avoid CLS
<Image src={card} alt="" width={640} height={400} sizes="(min-width: 1024px) 33vw, (min-width: 640px) 50vw, 100vw" className="aspect-[16/10] w-full object-cover" />
```

## Rules

- Use `next/image`. Provide `width`/`height` (or `fill` inside a container with a fixed aspect ratio) so space is reserved.
- `sizes` is mandatory for responsive layouts; it decides which variant downloads. Write it to match the actual layout (don't send 1920px to a 360px phone).
- `priority`: only the genuine above-the-fold LCP image (usually one per page). Never blanket.
- Formats: AVIF/WebP (enabled in framework config), SVG for logos/icons, PNG only where transparency is needed.
- Source assets: ~2x the largest rendered size, compressed (quality ~75-80). Don't ship 3000px originals for 600px slots. Flag > 200KB.
- Decorative -> `alt=""`; informative -> meaningful alt; avoid text in images.
- SVGs: optimize; inline only small icons; avoid enormous path-heavy SVG as a hero.
- Avoid CSS background images for LCP candidates (no preload discovery); use `<Image>`.
- Video: `preload="none"` + `poster`; `playsinline muted` for autoplay loops; reserve the aspect ratio.
- Remote images: allow-list hosts explicitly; prefer a CDN.
- `placeholder="blur"` for local hero images when it helps perceived load.
