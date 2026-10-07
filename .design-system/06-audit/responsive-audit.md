# Responsive audit

**Widths (minimum):** 320 · 375 · 390 · 414 · 768 · 1024 · 1280 · 1440 · 1920 (also 640 when tablet logic exists).
Method: DevTools device toolbar / browser pane resize; also landscape phones (e.g. 667x375); test 200% zoom.

### Horizontal overflow
- **Expected:** no horizontal scroll at any width.
- **Common problems:** fixed-width elements, long unbroken strings, wide tables/code/iframes, full-viewport-width elements plus scrollbar, negative margins, flex children that can't shrink.
- **How to debug:** console: `document.documentElement.scrollWidth > document.documentElement.clientWidth`; find offenders: `[...document.querySelectorAll('*')].filter(e=>e.getBoundingClientRect().right>innerWidth)`.
- **How to fix:** max-width 100%, allow flex children to shrink (`min-w-0`), break long words, scroll wrapper for tables, fluid widths.

### Text wrapping and headings
- **Expected:** no clipped/overflowing text; headings wrap cleanly; not oversized at 320.
- **Common problems:** long words/emails, uppercase tracking, fixed heights on text boxes.
- **How to debug:** inspect at 320; use long-content fixtures.
- **How to fix:** balanced wrapping, word breaking, min-height instead of height, adjust the project's clamp tokens.

### Buttons and touch targets
- **Expected:** >= 44x44px; full-width or wrapping groups on mobile; labels not truncated.
- **Common problems:** tiny icon buttons, buttons overflowing in a row, small close icons.
- **How to debug:** element size in DevTools; tap through at phone width.
- **How to fix:** `touch-target` token, wrapping button groups, full-width on mobile.

### Navigation
- **Expected:** mobile menu works (open/close/Esc/focus), tablet condensed, desktop full; no overlap at 768-1024.
- **Common problems:** nav breaks at in-between widths (800-1000), scroll lock not restored, sticky header covers anchors.
- **How to debug:** sweep widths continuously 320-1280.
- **How to fix:** choose the breakpoint by content width; scroll-margin on anchor targets.

### Images, media, cards, grids
- **Expected:** no distortion; fixed aspect; correct `sizes`; grids reflow 1/2/3-4 columns; 1-item and long-title cases fine.
- **Common problems:** stretched images, uneven card heights, orphan card in last row, huge images on mobile.
- **How to debug:** Network image size per width; fixtures with 1, 2, 7 items.
- **How to fix:** aspect ratio + object-fit; intrinsic grids; accurate `sizes`; line clamp where acceptable.

### Sections, containers, spacing
- **Expected:** consistent fluid gutters (`space-gutter`), content capped on large screens, rhythm preserved.
- **Common problems:** content stretched at 1920, cramped 320 gutters, mismatched section padding.
- **How to fix:** container tokens, `space-section`, max widths.

### Modals, forms, tables, footer, sticky elements
- **Expected:** modals usable on mobile (scrollable, reachable close); forms single column; tables scroll or restructure; footer stacks; sticky elements use <= ~20% of viewport height.
- **Common problems:** modal taller than viewport without scroll, keyboard covering fields, sticky bar + cookie banner stacking.
- **How to debug:** open at 320x568 and landscape; test on-screen keyboard.
- **How to fix:** max-height with scroll (dynamic viewport units), safe-area padding, limit sticky layers, z-index tokens.
