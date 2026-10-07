# Performance contract

Every project follows these standards. Performance is a design constraint, not a late audit.

## Standards

- Server Components by default; minimal client JavaScript.
- Optimized images (`next/image`, AVIF/WebP, correct `sizes`, dimensions reserved).
- Optimized fonts (`next/font`, few families and weights).
- Lazy loading below the fold; code splitting for heavy components.
- No unnecessary dependencies; no unnecessary third-party scripts; none on the critical path.
- No render-blocking resources.
- No layout shifts; reserve space for all media and async content.
- No request waterfalls; fetch in parallel; stream non-critical content.
- Prefer CSS animation (transform/opacity) when animation is warranted.
- Cache and statically render public content wherever possible.

## Targets (Core Web Vitals, 75th percentile mobile)

LCP <= 2.5s · INP <= 200ms · CLS <= 0.1. Also monitor FCP, TBT, TTFB, Speed Index.

## Honest scope

These are **targets and budgets, not promises**. Whether a deployed project hits them depends on hosting, backend latency, content, assets, traffic and third-party services. The design system's job is to remove avoidable causes of slowness and to define how to measure and fix the rest. Never claim "perfect" scores; report measured numbers.

## Process

1. Establish a baseline (lab + field where available) per important route.
2. Find the cause with tooling; do not guess.
3. Smallest fix; re-measure; check responsive, accessibility regressions.
4. Record before/after numbers.

See `core-web-vitals.md`, `budgets.md`, `images.md`, `fonts.md`, `javascript.md`, `third-party-scripts.md`, and `../06-audit/debug-workflow.md`.
