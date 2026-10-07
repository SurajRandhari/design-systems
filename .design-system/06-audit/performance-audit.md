# Performance and Core Web Vitals audit

**Always establish a baseline first.** Record per important route: TTFB, FCP, LCP (and which element), INP, CLS, TBT, Speed Index, JS execution, network requests, image/font loading, third-party scripts. Use a production build, mobile profile, throttled, cold cache; note tool and date. Prefer field data (CrUX / `web-vitals`) for final verdicts. Report measured numbers; never claim "perfect".

### LCP (<= 2.5s)
- **Expected:** LCP element known; hero image `priority` + `sizes` + modern format; text LCP not blocked by fonts/JS; no entrance animation delaying it.
- **Common problems:** lazy-loaded hero, oversized image, `priority` everywhere, client-rendered hero, slow TTFB.
- **How to debug:** DevTools Performance LCP breakdown (TTFB / load delay / load time / render delay); Lighthouse LCP insight.
- **How to fix:** attack the largest sub-part: server-render, prioritize/preload, resize/compress, remove animation, cache.

### CLS (<= 0.1)
- **Expected:** no unexpected shifts.
- **Common problems:** unsized images/embeds, late font swap, injected banners, mismatched skeleton sizes, hydration changes.
- **How to debug:** Performance panel Layout Shifts track; Rendering > Layout Shift Regions.
- **How to fix:** width/height or aspect-ratio, min-height, `next/font`, reserved slots.

### INP (<= 200ms), TBT, JavaScript
- **Expected:** fast interactions; first-load JS within budget; few, small client islands.
- **Common problems:** large client components, heavy dependencies, global third-party scripts, expensive handlers, re-render storms.
- **How to debug:** long tasks in Performance; bundle analyzer; React Profiler; count `"use client"` files.
- **How to fix:** shrink client boundary, dynamic import, lazy/remove third parties, debounce or transition, drop deps.

### FCP, TTFB, Speed Index
- **Expected:** FCP <= 1.8s; TTFB <= 0.8s.
- **Common problems:** dynamic rendering where static works, request waterfalls, blocking CSS/scripts, distant data region.
- **How to debug:** Network waterfall, server timing, cache headers.
- **How to fix:** static/ISR, `Promise.all`, Suspense streaming, CDN, nearer data.

### Images, fonts, third parties, network
- **Expected:** budgets in `../05-performance/budgets.md` met; <= 2 font files; no third-party on critical path.
- **Common problems:** 3000px images, many font weights, tag manager + chat + pixels in the root layout.
- **How to debug:** Network by size; filter third-party; Coverage tab.
- **How to fix:** see `../05-performance/images.md`, `../05-performance/fonts.md`, `../05-performance/third-party-scripts.md`.

Re-measure after each change; record before -> after.
