# Naming conventions

| Thing | Convention | Example |
|---|---|---|
| Component file and export | PascalCase `.jsx` | `HeroSection.jsx` |
| Page-section component | `{Name}Section` | `FeaturesSection.jsx` |
| Common group folder | PascalCase plural | `components/common/Buttons/` |
| Page component folder | lowercase, matches route/feature | `components/pricing/` |
| shadcn files | lowercase kebab (shadcn default) | `components/ui/dropdown-menu.jsx` |
| Route folders | lowercase kebab | `app/case-studies/page.js` |
| Dynamic segments | `[slug]` | `app/products/[slug]/page.js` |
| `lib` files | camelCase `.js` | `lib/utils/formatPrice.js` |
| Constants | UPPER_SNAKE values, camelCase file | `ROUTES` in `lib/constants/routes.js` |
| Hooks | `use` + PascalCase | `hooks/useMediaQuery.js` |
| Tokens | kebab-case semantic names | `primary-hover`, `radius-md`, `space-section` |
| Booleans | `is/has/should` prefix | `isOpen` |
| Event props / handlers | `onX` / `handleX` | `onSubmit`, `handleSubmit` |

- The same section name may exist in different page folders (`home/HeroSection`, `about/HeroSection`); the folder disambiguates, so the import path always shows it.
- Name by **purpose**, not appearance (`SecondaryButton`, not `GreyButton`; token `primary`, not `blue`).
- No barrel `index.js`; no `Component2`/`New*`/`Final*` names.
- TypeScript projects use the same names with `.tsx`/`.ts`.
