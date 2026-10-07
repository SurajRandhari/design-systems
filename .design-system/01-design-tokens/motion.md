# Motion contract

| Category | Tokens |
|---|---|
| Duration | `duration-fast` `duration-normal` `duration-slow` |
| Easing | `ease-standard` `ease-in` `ease-out` `ease-in-out` |

Values are project-specific. Typical shape: fast ~100-150ms (hover/focus), normal ~200-300ms (menus, small movement), slow ~350-500ms (large entrances). `ease-standard` is the default curve; `ease-out` for entrances, `ease-in` for exits, `ease-in-out` for on-screen movement.

## Rules

- Animate `transform` and `opacity` only. Never `top/left/width/height/margin`.
- Prefer CSS transitions/animations over JS libraries. Add a JS animation library only if CSS cannot do it, and load it lazily.
- Specify properties explicitly (`transition-[transform,opacity]`), not `transition-all`.
- Nothing above the fold starts hidden or animates in before LCP.
- Honour `prefers-reduced-motion` globally; large movement needs a reduced alternative.
- Animation communicates hierarchy, state or interaction. Don't animate everything.
- Component states are tokenized the same way: hover, focus-visible, active, disabled, loading (`aria-busy`), error (`aria-invalid`).
