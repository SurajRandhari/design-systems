# Accessibility contract (WCAG 2.2 AA)

Accessibility is part of the design system, not a late audit. Every project supports: semantic HTML, keyboard navigation, visible focus, correct labels, heading hierarchy, sufficient contrast, alt text, accessible buttons and links, reduced motion, touch-friendly controls.

| Requirement | Rule |
|---|---|
| Semantics | `<button>` for actions, `<a>` for navigation, landmarks (`header nav main footer`), lists for lists. **Never `<div onClick>`.** |
| Headings | One `h1`; no skipped levels; headings describe content, not styling. Change look with type tokens (`text-h*`), not by picking a different element. |
| Keyboard | Everything operable with Tab/Enter/Space/Esc/arrows; logical order; no traps; skip link to main content. |
| Focus | Always visible (>= 3:1). Never remove outlines without a replacement. Focus moves into dialogs and returns after close. |
| Labels | Every input has a `<label>`; icon-only buttons have `aria-label`; links have meaningful text (not "click here"). |
| Alt text | Informative images: describe purpose. Decorative: `alt=""`. Decorative SVG icons: `aria-hidden="true"`. |
| ARIA | Only when native HTML can't express it. Prefer shadcn/Radix patterns. Wrong ARIA is worse than none. |
| Contrast | Text 4.5:1 (large 3:1); UI components and focus 3:1. Don't rely on color alone. |
| Touch targets | >= 44x44 CSS px (`touch-target` token); >= 8px between targets. (WCAG 2.2 minimum is 24px; the contract uses 44.) |
| Motion | Respect `prefers-reduced-motion`; no autoplay motion > 5s without a pause control; nothing flashes > 3/s. |
| Zoom/reflow | Works at 200% zoom and 320px width without 2-D scrolling; never disable user zoom; rem-based type. |
| Forms | Errors in text, linked via `aria-describedby`, announced via a live region; `autocomplete` attributes; don't clear input on error. |
| Media | Captions for speech; no autoplay with sound. |
| Language | `<html lang>`; mark language changes. |
| Status messages | `role="status"` / `aria-live="polite"` for async results (toasts, counts). |

## Testing
Keyboard-only pass; screen-reader smoke test (NVDA/VoiceOver) on key flows; axe; Lighthouse accessibility; contrast checker. See `../06-audit/accessibility-audit.md`.
