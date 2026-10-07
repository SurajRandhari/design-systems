# UI audit

### Token usage
- **Expected:** all color/type/spacing/radius/shadow/motion/z-index come from semantic tokens.
- **Common problems:** `text-[#...]`, palette names (`bg-blue-500`), `mt-[37px]`, `shadow-[...]`, inline style colors, hardcoded px font sizes.
- **How to debug:** search the codebase for arbitrary-value brackets, hex colors, `style={{`.
- **How to fix:** replace with a semantic utility; if a value repeats 3+ times, propose a token (name per `../01-design-tokens/token-architecture.md`).

### Typography
- **Expected:** fluid type tokens; one `h1`; balanced headings; body >= 1rem on mobile; prose 45-75ch.
- **Common problems:** huge mobile headings, orphans, px-sized text, long all-caps paragraphs.
- **How to debug:** computed font-size at 320/768/1440; check wraps.
- **How to fix:** use `text-h*` tokens; adjust the project's clamp values, not per-page overrides.

### Spacing and rhythm
- **Expected:** `space-section`, `space-gap`, `space-stack`, `space-gutter` used consistently.
- **Common problems:** ad-hoc margins, double margins, cramped mobile, huge desktop gaps.
- **How to debug:** box-model overlay; compare adjacent sections.
- **How to fix:** parent-owned gap/stack spacing; fluid tokens; remove per-child margins.

### Component states
- **Expected:** hover, focus-visible, active, disabled, loading, empty, error all designed.
- **Common problems:** missing disabled style; no empty state; spinner shifts layout; hover-only info.
- **How to debug:** force states in DevTools; mock empty/error data; throttle network.
- **How to fix:** add the states; skeletons sized like final content; touch alternatives.

### Visual consistency
- **Expected:** same radius/shadow/elevation per component type; consistent icon size/stroke; brand tokens only.
- **Common problems:** mixed radii, random shadows, off-palette colors, mixed icon sets.
- **How to debug:** side-by-side page comparison; search for raw values.
- **How to fix:** swap to tokens; consolidate duplicates into one component.

### Dark mode (if the project has it)
- **Expected:** only semantic token values switch; contrast holds; shadows/images remain legible.
- **Common problems:** hardcoded white/black, low-contrast muted text, invisible borders.
- **How to debug:** toggle the theme; run a contrast checker.
- **How to fix:** use semantic utilities; adjust dark token values.
