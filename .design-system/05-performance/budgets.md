# Performance budgets

Starting points. Each project records its own budgets, tunes them to its type (marketing site vs. dashboard), and justifies exceptions.

| Metric | Default budget |
|---|---|
| LCP / INP / CLS (p75, mobile) | <= 2.5s / <= 200ms / <= 0.1 |
| FCP / TTFB | <= 1.8s / <= 0.8s |
| TBT (lab) | <= 200ms |
| First-load JS per route | <= 170KB gzip target; investigate > 250KB |
| Total CSS | <= 60KB |
| Font files | <= 2 files, <= 100KB each (woff2) |
| Above-the-fold image | <= 200KB each, correct `sizes` |
| Third-party scripts on the critical path | 0 |
| Client components | Tracked; any whole-page client component is flagged |

## What to monitor

JavaScript bundle size · CSS size · image sizes · font size · third-party scripts · number of network requests · largest assets · client component count.

## Flags (investigate before accepting)

Unusually large assets · unnecessary dependencies · large client bundles · whole-page client components · global third-party scripts · images served larger than their rendered size · more than two font files.

## How to measure

Production build only. Lab: Lighthouse (mobile throttled), DevTools Performance. Field: CrUX / PageSpeed Insights / `web-vitals` reporting. Bundle: the framework's build route table and a bundle analyzer. Record route, device profile, value, date.

Budgets are checked at every audit (`../06-audit/performance-audit.md`) and before release.
