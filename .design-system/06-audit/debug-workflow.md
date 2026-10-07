# Debug contract

```
Reproduce (exact route, width, device, state, data)
   ↓
Identify route
   ↓
Identify component
   ↓
Identify layer: UI / CSS / JS / API / database / network
   ↓
Measure baseline (numbers, not feelings)
   ↓
Find root cause
   ↓
Apply smallest fix
   ↓
Measure again
   ↓
Check regression: responsive (320 -> 1920), accessibility (keyboard, contrast, axe), Core Web Vitals, lint, production build
```

## Classifying quickly

| Symptom | Look at |
|---|---|
| Layout broken at some width | CSS: box model, overflow finder (`responsive-audit.md`) |
| Slow first paint / LCP | Network waterfall, TTFB, LCP breakdown, image/font |
| Janky interaction / INP | Long tasks, client component size, handlers |
| Content wrong/missing | `lib/api` output, server logs, caching |
| Intermittent / env-specific | Throttling, cache headers, hydration mismatch |
| Hydration warning | Server/client markup differ (dates, `window`, random ids) |

## Rules

- **Never optimize on assumption.** No baseline, no fix.
- One change at a time; re-measure each.
- Fix the root cause, not the symptom; smallest change that works; don't refactor unrelated code.
- Lab tools find causes; field data confirms impact.
- Record: issue, route, baseline, cause, fix, after, regressions checked.
- Measure performance on a production build only; development-mode numbers are meaningless.
