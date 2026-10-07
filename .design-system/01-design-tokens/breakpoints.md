# Breakpoint contract

One conceptual strategy for all projects: **four tiers, mobile-first, `min-width`**.

| Tier | Width range | Intent |
|---|---|---|
| Mobile | 320 - 639 | Base styles. Single column, stacked, touch-first |
| Tablet | 640 - 1023 | Two-column / condensed navigation |
| Desktop | 1024 - 1535 | Full navigation, multi-column |
| Large desktop | 1536+ (validate at 1920) | Capped content width; extra space becomes whitespace/scale |

Standard thresholds (rem so they respect user font size): `sm` 40rem (640) · `md` 48rem (768) · `lg` 64rem (1024) · `xl` 80rem (1280) · `2xl` 96rem (1536) · `3xl` 120rem (1920, optional). Projects implement the syntax of their framework but keep these names and thresholds.

Container widths (semantic): `container-page` (~80rem), `container-narrow` (~56rem), `container-prose` (~42rem, 45-75ch).

## Rules

- Write base (mobile) styles first; breakpoints only **add**.
- Use the fewest breakpoints necessary; prefer fluid tokens (`clamp`), intrinsic grids (`auto-fit/minmax`) and container queries.
- Choose a breakpoint where content breaks, not at a device name.
- Always validate: 320, 375, 390, 414, 768, 1024, 1280, 1440, 1920 (+640).
- Use dynamic viewport units (`dvh`) rather than `100vh` for full-height layouts.
