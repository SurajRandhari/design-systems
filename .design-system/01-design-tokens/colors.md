# Color token contract

Every project MUST define all tokens below. Values are project-specific.

| Group | Tokens |
|---|---|
| Primary | `primary` `primary-hover` `primary-active` `primary-disabled` `primary-foreground` |
| Secondary | `secondary` `secondary-hover` `secondary-active` `secondary-disabled` `secondary-foreground` |
| Tertiary | `tertiary` `tertiary-hover` `tertiary-active` `tertiary-foreground` |
| Background | `background` `background-secondary` `background-tertiary` |
| Foreground (text) | `foreground` `foreground-secondary` `foreground-muted` `foreground-inverse` `heading` |
| Border | `border` `border-secondary` `border-strong` |
| Status | `success` `warning` `error` `info` |

Recommended companions (define when the UI needs them): `*-foreground` and `*-subtle` for each status color (`error-subtle` tinted background, `error-foreground` text on solid), `input` (form-control border), `ring` (focus outline), `background-inverse`.

## Meaning

- `primary`: main brand action color (buttons, key links). `-foreground` is the text/icon color ON a primary surface.
- `secondary`: supporting action color. `tertiary`: low-emphasis/accent.
- `background` = page surface; `-secondary` = alternating section/card surface; `-tertiary` = deeper/inset surface.
- `foreground` = default body text; `-secondary` = supporting text; `-muted` = non-essential text (still must pass contrast); `-inverse` = text on dark/primary surfaces. `heading` = heading color.
- `border` default; `-secondary` subtle dividers; `-strong` emphasized/inputs.
- Status colors for feedback; never rely on color alone.

## Utility usage (framework mapping in `../07-framework/tailwind.md`)

```
bg-primary  text-primary  border-primary  hover:bg-primary-hover  text-primary-foreground
bg-background  bg-background-secondary  text-foreground  text-foreground-muted  text-heading
border-border  border-border-strong  text-error  bg-success
```

### Reserved-name clarifications

- `text-body` is the **font-size** utility (typography). Body text *color* is `text-foreground`.
- `text-muted` is not a color utility; use `text-foreground-muted`.
- `text-secondary` = the secondary **brand** color used as text; supporting body text is `text-foreground-secondary`.

## Rules

- Components never use palette names (`blue-500`), hex, rgb or hsl.
- Contrast (WCAG 2.2 AA): text 4.5:1 (large 3:1); UI boundaries and focus indicators 3:1. The project must verify every `foreground*` on `background*` and `*-foreground` on its surface.
- Disabled tokens exist so disabled state is styled by token, not by opacity hacks alone.
- Replacing the entire brand palette must not require editing any component.
