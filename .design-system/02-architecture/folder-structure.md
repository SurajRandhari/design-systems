# Universal folder architecture (the standard for every project)

Documented here only. This repository does not contain these folders.

```
project/
├── app/            routes only (Next.js App Router)
├── components/     all UI
│   ├── ui/         shadcn primitives ONLY
│   ├── layout/     Container, Section, Header, Footer, PageWrapper
│   ├── common/     shared reusable components, grouped (Buttons/, Cards/, Forms/, Icons/, Modals/, Navigation/)
│   ├── home/       page-specific components
│   ├── about/
│   ├── pricing/
│   ├── admin/      admin-panel components (same architecture)
│   └── ...         one folder per page or feature area
├── lib/            application logic (no UI)
│   ├── api/        data access: DB / external APIs
│   ├── data/       static and configuration data
│   ├── constants/  routes, site constants
│   ├── config/     fonts, env parsing, feature flags
│   └── utils/      pure helpers (formatDate, formatPrice, cn ...)
├── hooks/          shared client hooks (only when reused)
├── types/          shared types / typedefs (only if used)
└── public/         static assets (optimized images, icons, og images)
```

## Placement rules

| Question | Answer |
|---|---|
| Used by one page only | `components/<page>/` |
| Used by 2+ pages | `components/common/<Group>/` |
| Page chrome (header, footer, containers) | `components/layout/` |
| shadcn primitive | `components/ui/` |
| Admin-only UI | `components/admin/` |
| Fetches data / talks to DB | `lib/api/` |
| Static content, nav links, FAQs | `lib/data/` |
| Route strings, site-wide constants | `lib/constants/` |
| Fonts, env, flags | `lib/config/` |
| Pure function | `lib/utils/` |
| Reused client-side stateful logic | `hooks/` |

## Rules

- **No barrel files**: no `index.js` in `components/*`. Import directly: `import HeroSection from "@/components/home/HeroSection"`.
- Place a component at the narrowest scope that holds; promote to `common/` when a second consumer appears.
- `components/ui/` is shadcn's location; no business components there, no competing primitive folder.
- Application logic lives in `lib/`, never in `components/lib/`.
- Create folders when the first file needs them. No empty folders, no catch-all `utils.js`.
- Route folders hold only route files (`page`, `layout`, `loading`, `error`, `not-found`, route handlers) and route-private helpers.
- Same architecture for every project type: marketing, SaaS, admin, dashboard, e-commerce.
- shadcn alias note: if `lib/utils/` is a folder, point shadcn's `utils` alias at a file inside it (e.g. `@/lib/utils/cn`).
