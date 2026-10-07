# Audit checklist (reusable across every project)

Every project is audited for: **UI · Responsive · Accessibility · Performance · Core Web Vitals · SEO · Architecture · Code Quality.**
Each audit file uses the same shape: **Check · Expected behavior · Common problems · How to debug · How to fix.**

| Discipline | File |
|---|---|
| UI | `ui-audit.md` |
| Responsive | `responsive-audit.md` |
| Accessibility | `accessibility-audit.md` |
| Performance + Core Web Vitals | `performance-audit.md` (CWV targets in `../05-performance/core-web-vitals.md`) |
| SEO | `seo-audit.md` |
| Architecture | `architecture-audit.md` |
| Code quality | `code-quality-audit.md` |
| Debugging process | `debug-workflow.md` |

## When to run what

| Trigger | Run |
|---|---|
| New component | UI, Responsive (component), Accessibility, Code quality |
| New page / route | All; record the likely-LCP element |
| Dependency or script added | Performance, Architecture, Code quality |
| Token or global style change | UI, Responsive (spot-check key pages), Accessibility (contrast) |
| Adopting the contract in an existing project | Architecture first; record conflicts before changing anything |
| Pre-release | All, on every important route |

## Master checklist

- [ ] **Architecture:** files in contract folders; no barrels; logic in `lib/`; shadcn only in `ui/`; server by default; no data access in presentation components; public URLs unchanged; no accidental `noindex`
- [ ] **UI:** semantic tokens only; consistent spacing/type/radius/shadow; all states designed (hover, focus, active, disabled, loading, empty, error)
- [ ] **Responsive:** 320 · 375 · 390 · 414 · 768 · 1024 · 1280 · 1440 · 1920 with no horizontal scroll and intentional layouts per tier
- [ ] **Accessibility:** keyboard, visible focus, labels, headings, alt, contrast, touch targets, reduced motion
- [ ] **Performance / CWV:** baseline recorded; LCP <= 2.5s, INP <= 200ms, CLS <= 0.1 (measured, not assumed); budgets respected; no global third-party scripts
- [ ] **SEO:** title, description, canonical, robots, OG/Twitter, structured data, sitemap, one `h1`
- [ ] **Code quality:** lint passes; production build passes; no needless abstractions or dependencies
- [ ] Results recorded (route, width, tool, value, date)
