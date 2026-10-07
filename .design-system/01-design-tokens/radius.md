# Radius contract

Tokens: `radius-sm` `radius-md` `radius-lg` `radius-xl` `radius-2xl` `radius-full`. Values are project-specific (a sharp brand may use 0-4px; a soft brand 8-24px). Utilities: `rounded-sm` ... `rounded-full`.

| Token | Typical use |
|---|---|
| `radius-sm` | Badges, chips |
| `radius-md` | Buttons, inputs |
| `radius-lg` | Cards |
| `radius-xl` | Large cards, dialogs |
| `radius-2xl` | Feature panels, hero media |
| `radius-full` | Avatars, pills |

## Rules

- A project may derive all sizes from one base value so the whole feel changes in one place.
- Nested radii: inner radius = outer radius - padding.
- No arbitrary radii (`rounded-[13px]`).
