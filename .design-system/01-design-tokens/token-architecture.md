# Token architecture and naming contract

This repository defines token **names and categories**. Each project defines the **values**.

## Three layers

```
Primitive values     raw scale: palette steps, base sizes        (project-private; never used by components)
        ↓
Semantic tokens      meaning: primary, foreground, radius-md     (THE CONTRACT; names fixed)
        ↓
Components           consume semantic tokens only: bg-primary
```

- **Primitive** examples (names are project's choice): `palette-brand-600`, `palette-neutral-900`.
- **Semantic** tokens are CSS custom properties named exactly as in this folder (`--primary`, `--foreground-muted`, `--radius-md`, `--font-h1`...).
- **Components** never reference primitives, and never contain raw values.
- Re-branding = change semantic-token values (or the primitives they point to). Zero component edits.

## Example: same names, different values (documentation only)

```
Project A                       Project B
--primary: #2563eb;             --primary: #059669;
--font-h1: clamp(2.5rem,4vw,4rem);   --font-h1: clamp(2.25rem,3.5vw,3.5rem);
--radius-md: 0.5rem;            --radius-md: 0.25rem;
```
Both projects write `bg-primary`, `text-h1`, `rounded-md`. Components don't know the value.

## Naming rules

1. Name by **role**, not appearance: `primary`, not `blue`; `foreground-muted`, not `gray-500`.
2. Pattern: `{role}[-{variant}][-{state}]` -> `primary`, `primary-hover`, `primary-foreground`, `background-secondary`.
3. States: `-hover`, `-active`, `-disabled`. Content-on-surface: `-foreground`. Tint surface: `-subtle` (optional for status).
4. Scales use t-shirt sizes: `xs sm md lg xl 2xl`, plus `full` for radius.
5. kebab-case only. CSS variable = `--` + token name. Utility = framework mapping (see `../07-framework/tailwind.md`).
6. A new token needs: a role, a name that fits the pattern, a dark-mode value if dark mode exists, and an entry in the project's token list. Don't add one-off tokens for single uses.
7. If a raw value repeats 3+ times, it should become a token.

## Required categories (every project must define all)

| Category | File |
|---|---|
| Color | `colors.md` |
| Typography | `typography.md` |
| Spacing | `spacing.md` |
| Shadows | `shadows.md` |
| Radius | `radius.md` |
| Motion | `motion.md` |
| Z-index | `z-index.md` |
| Breakpoints | `breakpoints.md` |

Dark mode, if a project has it, overrides **semantic values only**; token names stay identical.
