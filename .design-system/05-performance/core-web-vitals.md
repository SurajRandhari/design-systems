# Core Web Vitals

Targets (75th percentile, mobile): **LCP <= 2.5s · INP <= 200ms · CLS <= 0.1**. Also monitor FCP, TBT, Speed Index, TTFB. The goal is a genuinely fast site, not a green Lighthouse score. Field data (CrUX / `web-vitals`) beats lab data. These are targets, not guarantees: results depend on hosting, backend, content, assets, traffic and third parties (see `performance-contract.md`).

## LCP: Largest Contentful Paint

1. Identify the LCP element per important route (usually hero heading, hero image, product image, video poster). Record it in the page's audit notes.
2. Hero image: `next/image` with `priority` (or `fetchPriority="high"`), correct `sizes`, AVIF/WebP, intrinsic dimensions. **Only the single LCP image gets `priority`.**
3. Text LCP: render in server HTML; font via `next/font` (`display: swap`); no animation delaying it (no opacity-0 initial state).
4. Remove render-blocking: no sync third-party scripts in `<head>`; no CSS `@import` chains; keep CSS small.
5. Improve TTFB: static/ISR, CDN, parallel fetches, no waterfalls.
6. Don't lazy-load above-the-fold media. Avoid huge SVGs and hero video autoload (poster + load on interaction/visibility).

## CLS: Cumulative Layout Shift

- Always size media: width/height or aspect ratio. Same for iframes/embeds/ads.
- `next/font` for size-adjusted fallbacks; avoid late font swaps that reflow.
- Skeletons/min-height for async content; never insert content above existing content after load (banners, cookie bars -> overlay or reserved slot).
- Carousels: fixed height/aspect; animate with `transform`, not layout properties.
- Don't change display/size on hydration (render the same on server and client).

## INP: Interaction to Next Paint

- Less JS: Server Components, small client islands, remove unused dependencies.
- Keep handlers fast (<50ms); defer heavy work (transitions, idle callbacks, workers); debounce input handlers.
- Avoid unnecessary re-renders, effects and listeners; don't store derived data in state.
- Split long tasks; dynamic-import heavy widgets; avoid synchronous layout reads in loops.
- Third-party scripts are a top INP offender: lazy-load (`third-party-scripts.md`).

## FCP / TBT / Speed Index / TTFB

FCP: small critical CSS, no blocking scripts, fast TTFB. TBT: reduce main-thread JS (bundle, hydration, third parties). Speed Index: progressive rendering via streaming and sized placeholders. TTFB: caching/CDN, data region near users, avoid dynamic rendering where static works.

## Tooling

Lighthouse (mobile), PageSpeed Insights (field), DevTools Performance and Insights, the `web-vitals` library, WebPageTest. Always record: route, device/throttling, cold/warm cache, value, date.
