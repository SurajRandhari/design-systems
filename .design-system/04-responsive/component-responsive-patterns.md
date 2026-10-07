# Component responsive patterns

Companion to `responsive-contract.md`. Every reusable component declares its behavior for **Mobile / Tablet / Desktop / Large desktop**. Components adapt intentionally; they are not shrunken desktop layouts.

**Validation widths:** 320 · 375 · 390 · 414 · 640 · 768 · 1024 · 1280 · 1440 · 1920.

| Component | Mobile (base) | Tablet | Desktop | Large desktop |
|---|---|---|---|---|
| Hero | Single column; text first, media below at a fixed aspect ratio; CTAs full-width stacked | Balanced stacked/split; CTAs inline | Two columns (text / media) | Container capped; larger media, more whitespace |
| Navigation | Logo + menu button -> full-screen or side sheet; 44px items | Condensed: key links + "More"/menu | Full inline nav + CTA | Same; wider spacing |
| Cards grid | 1 column | 2 columns | 3 (4 if content is short) | 4 max; never exceed container |
| Feature rows | Stacked, image on top | Stacked or 2-col | Alternating 2-col | Capped |
| Tables | Stacked/card layout or horizontal scroll inside its own wrapper | Scroll or full | Full table | Full |
| Forms | Single column, full-width fields, large targets | 2-col for short fields | Same + side help | Capped width |
| Modal | Bottom sheet / full screen | Centered, medium width | Centered | Same |
| Footer | Stacked lists / accordions | 2 columns | 4 columns | Capped |
| Sticky elements | Minimal (don't eat viewport) | Limited | Allowed (header, TOC) | Allowed |
| Dashboards / admin | Single column widgets; tables scroll; filters in a sheet | 2 columns | Multi-column with side nav | Capped, denser grids |

## Beyond "just add columns"
For every grid check: content length extremes (long titles/words), image ratios, button wrapping, heading wrapping (balanced), spacing, touch targets (>= 44px), vertical rhythm, and the 1-item / 2-item / many-item cases.

## Hard rules
- No horizontal page scroll at any width.
- Flex/grid children holding text can shrink (`min-w-0`); long strings wrap; media never exceeds its container.
- No fixed pixel widths for containers; use fluid width with a max width.
- Full-height layouts use dynamic viewport units; respect safe areas for fixed bars.
- Hover-only affordances need touch/keyboard equivalents.
- Content stays legible at 200% zoom and larger user font sizes.
