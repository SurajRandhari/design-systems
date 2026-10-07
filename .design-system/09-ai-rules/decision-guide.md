# Decision guide: questions an agent must be able to answer

## Where does this component belong?
- shadcn primitive -> `components/ui/`
- Layout/chrome (header, footer, container, section) -> `components/layout/`
- Used by one page/feature -> `components/<page>/` (admin -> `components/admin/`)
- Used by 2+ pages -> `components/common/<Group>/` (Buttons, Cards, Forms, Icons, Modals, Navigation)
- Import directly; never create `index.js` barrels.

## Where does this API / data / constant / config / helper belong?
- Talks to DB or external API -> `lib/api/<resource>`
- Static content or config data (nav links, FAQs) -> `lib/data/`
- Fixed values (routes, site info) -> `lib/constants/`
- Env-derived config, fonts, feature flags -> `lib/config/`
- Pure helper -> `lib/utils/`
- Reused stateful client logic -> `hooks/`; shared types -> `types/`

## Server or Client Component?
Server unless it needs state, effects, refs, browser APIs, client event-driven interactivity, or a client-only library. If yes, make only the interactive leaf a client island and keep the surrounding section on the server.

## Which token should I use?
- Action surface: `bg-primary` / `secondary` / `tertiary` (+ `-hover/-active/-disabled`), text on it `-foreground`.
- Page/section surface: `bg-background`, `-secondary`, `-tertiary`. Body text `text-foreground`; supporting `-secondary`; non-essential `-muted`; headings `text-heading`.
- Lines: `border-border`, `-secondary`, `-strong`. Feedback: `success/warning/error/info`.
- Type: `text-display|h1..h6|body-lg|body|body-sm|label|caption|button`. Spacing: `space-gutter|section|gap|stack|component-*`. Depth: `shadow-xs..xl`; corners `rounded-sm..2xl|full`; motion `duration-*`/`ease-*`; layers `z-*`.
- No matching token? Propose a new semantic token. Never hardcode.

## How should this behave on mobile / tablet / desktop?
- **Mobile (base):** single column, stacked, mobile navigation, full-width primary actions, >= 44px targets, minimal sticky UI, no overflow.
- **Tablet:** 2 columns / balanced split, condensed navigation, inline actions.
- **Desktop:** multi-column (3-4 grid when content allows), full navigation, hover affordances plus touch/keyboard equivalents.
- **Large desktop:** capped container, whitespace and larger media instead of stretched content.
- Details per component: `../04-responsive/component-responsive-patterns.md`.

## How should I optimize this image?
`next/image`; AVIF/WebP; set width/height or aspect ratio; write accurate `sizes`; `priority` only if it is the single likely-LCP image, otherwise lazy; right-size the source (~2x rendered max) and compress; meaningful `alt` (or `alt=""` if decorative). See `../05-performance/images.md`.

## How should I debug this performance issue?
Reproduce -> identify route -> identify component -> identify layer (UI/CSS/JS/API/DB/network) -> measure baseline -> find root cause -> smallest fix -> measure again -> check regressions (responsive, accessibility, CWV) -> lint and build. Never optimize on assumption. See `../06-audit/debug-workflow.md`.

## Should I add this dependency / wrapper / hook / provider?
Only if you can name the concrete problem it solves today and have checked its cost. Default answer: no.
