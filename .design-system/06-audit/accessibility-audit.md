# Accessibility audit (WCAG 2.2 AA)

### Semantics and landmarks
- **Expected:** `header/nav/main/footer`, one `h1`, ordered headings, lists for lists, correct buttons vs links.
- **Common problems:** `<div onClick>`, links used as buttons (`href="#"`), skipped heading levels, multiple `h1`.
- **How to debug:** DevTools Accessibility tree; axe; headings-map extension.
- **How to fix:** swap to native elements; heading level by structure, size via type tokens.

### Keyboard and focus
- **Expected:** logical Tab order; visible focus everywhere; no traps; Esc closes overlays; focus returns; skip link works.
- **Common problems:** outline removed without replacement, focus hidden under sticky header, custom controls not focusable.
- **How to debug:** unplug the mouse; Tab through the page.
- **How to fix:** restore a global focus style; scroll-margin for sticky headers; use Radix/shadcn primitives; `tabIndex` only where needed.

### Names, labels, alt
- **Expected:** every control has an accessible name; correct alt; decorative hidden.
- **Common problems:** icon-only buttons without label, placeholder-as-label, "click here", missing/redundant alt.
- **How to debug:** axe name rules; screen-reader read-through.
- **How to fix:** `aria-label`, `<label>`, descriptive link text, `alt=""` for decoration.

### Color contrast
- **Expected:** text 4.5:1 (large 3:1); UI/focus 3:1; no color-only meaning.
- **Common problems:** muted text on secondary background, brand color with white text < 4.5, disabled states, placeholders.
- **How to debug:** DevTools contrast ratio; axe; test dark mode too.
- **How to fix:** repoint the semantic token to a darker/lighter value; add icon/text to status.

### Touch targets and zoom
- **Expected:** targets >= 44px; 200% zoom / 320px reflow works; pinch zoom allowed.
- **Common problems:** zoom disabled, px text ignoring browser settings, tiny close buttons.
- **How to fix:** `touch-target` token, rem units, remove zoom restrictions.

### Forms and feedback
- **Expected:** labels, `aria-describedby` for help/errors, `aria-invalid`, live-region errors, correct `autocomplete` and `type`.
- **Common problems:** errors only in red, errors not announced, required not stated in text.
- **How to fix:** add text + icon; alert role/live region; `aria-required`.

### Motion and media
- **Expected:** reduced-motion respected; no autoplay > 5s without control; captions.
- **How to debug:** DevTools Rendering -> emulate `prefers-reduced-motion`.
- **How to fix:** motion-safe variants; pause control; remove autoplay.

**Tools:** axe DevTools, Lighthouse accessibility, Accessibility Insights, NVDA/VoiceOver smoke tests on primary flows.
