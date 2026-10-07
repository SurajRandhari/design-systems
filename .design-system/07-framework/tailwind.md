# Tailwind CSS contract

Tailwind is the primary styling system for every project. Tailwind classes must **consume the design tokens**.

## Wiring principle (project-side, described not implemented)

```
Primitive values --> Semantic CSS variables (--primary ...) --> Tailwind theme mapping --> utilities (bg-primary)
```

- Each project defines its semantic tokens as CSS custom properties (light, and dark if applicable) and maps them into Tailwind's theme (CSS-first `@theme` in Tailwind v4; `theme.extend` in v3).
- The Tailwind default palette should be disabled or unused so raw colors (`bg-blue-500`) cannot be written.
- Dark mode, if used, overrides semantic values only (class or attribute strategy); components don't change.

## Token -> utility map (the contract)

| Token category | Utilities |
|---|---|
| Color | `bg-{token}` `text-{token}` `border-{token}` `ring-{token}` (e.g. `bg-primary`, `hover:bg-primary-hover`, `text-foreground-muted`, `border-border-strong`, `text-heading`) |
| Typography | `text-display` `text-h1`..`text-h6` `text-body-lg` `text-body` `text-body-sm` `text-label` `text-caption` `text-button` |
| Spacing | `p-*` `m-*` `gap-*` `space-*` from the scale; semantic: `px-gutter` `py-section` `gap-gap` `space-y-stack` |
| Shadow | `shadow-xs` ... `shadow-xl` |
| Radius | `rounded-sm` ... `rounded-2xl` `rounded-full` (token `radius-*`) |
| Motion | `duration-fast|normal|slow` `ease-standard|in|out|in-out` |
| Z-index | `z-base` `z-dropdown` `z-sticky` `z-header` `z-overlay` `z-modal` `z-toast` |
| Breakpoints | `sm: md: lg: xl: 2xl:` (+ optional `3xl:`) |

## Rules

- **Mobile-first**: unprefixed classes are mobile; prefixed classes add at larger widths. Don't write desktop classes then override down.
- **Semantic tokens only** in components. No `text-[#123456]`, `mt-[37px]`, `shadow-[...]`, `z-[9999]`, `rounded-[13px]`.
- Arbitrary values only when genuinely one-off and no token fits (e.g. a specific `aspect-[4/3]`); if used 3+ times, create a token/utility.
- **State variants**: `hover:` `focus-visible:` `active:` `disabled:` `aria-[invalid=true]:` `data-[state=open]:` `group-hover:`; always include `focus-visible`.
- **Reduced motion**: `motion-safe:` / `motion-reduce:` for non-trivial movement.
- **Responsive typography/spacing**: fluid tokens; avoid sprinkling `text-sm md:text-base lg:text-lg`.
- **Custom utilities** (`@utility`/plugins): only for repeated patterns (e.g. page container, focus ring, touch target); name them semantically.
- **Class strings**: don't duplicate long strings; extract a component or a variant (`cva`) when repeated 3+ times. Merge conditional classes with a merge helper so `className` overrides work.
- **Dark mode (if applicable)**: use semantic utilities; avoid `dark:` per-element color overrides.
- **Reserved names**: `text-body` is font size (not color); body text color is `text-foreground`.
- Content/readability utilities: prose width via container-prose token; `min-w-0` on text-bearing flex/grid children; `break-words` for user content.
