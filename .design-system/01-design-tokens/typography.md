# Typography contract

Every project exposes the same semantic type names. Sizes are project-specific.

| Semantic name | Utility | Role |
|---|---|---|
| `display` | `text-display` | Hero statement only |
| `h1` | `text-h1` | Page title (one per page) |
| `h2` | `text-h2` | Section title |
| `h3` | `text-h3` | Subsection / card title |
| `h4` `h5` `h6` | `text-h4` `text-h5` `text-h6` | Lower headings |
| `body-lg` | `text-body-lg` | Lead paragraph |
| `body` | `text-body` | Default text |
| `body-sm` | `text-body-sm` | Secondary text |
| `label` | `text-label` | Form labels, UI labels |
| `caption` | `text-caption` | Captions, meta |
| `button` | `text-button` | Button text |

Each size token is a CSS variable (`--font-h1`, `--font-body`, ...). Projects may also define `--leading-*` and `--tracking-*` per name, and font families `--font-family-primary`, `--font-family-secondary`, and weights `--font-weight-regular|medium|semibold|bold`.

## Rules

- **rem, not px.** Respects the user's browser font size.
- **Fluid with `clamp()`**: `clamp(min, rem-intercept + vw-slope, max)`. Always include a rem term in the preferred value so browser zoom still scales text (WCAG 1.4.4).
- Example shape (values illustrative; project decides): `--font-h1: clamp(2.25rem, 1.6rem + 2.4vw, 3.75rem);`
- Validate type at 320, 375, 390, 414, 768, 1024, 1440, 1920: no overflow, no awkward wraps, headings not oversized on mobile (rule of thumb: `display` <= ~2.75rem and `h1` <= ~2.5rem at 320px).
- Body text >= 1rem on mobile for primary content.
- Line length for prose 45-75 characters (use a prose max width token/utility).
- Heading hierarchy is semantic: choose `h1-h6` elements by document structure; change *appearance* with `text-*` utilities, never by skipping levels.
- Long words/user content must wrap (`overflow-wrap: break-word`); headings use balanced wrapping where supported.
- Load only the font weights actually used; prefer one variable font family (see `../05-performance/fonts.md`).
- No `text-[22px]`-style arbitrary sizes.
