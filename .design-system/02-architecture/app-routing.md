# App Router contract

All projects use the Next.js App Router. Admin sections are ordinary routes.

```
app/
├── layout.js
├── page.js
├── globals.css
├── about/
│   └── page.js
├── contact/
│   └── page.js
├── pricing/
│   └── page.js
├── products/
│   └── [slug]/
│       └── page.js
└── admin/
    ├── layout.js            (admin shell, auth guard)
    ├── page.js
    ├── users/
    │   └── page.js
    ├── settings/
    │   └── page.js
    └── reports/
        └── page.js
```

## Rules

- `admin` is **not** a separate architecture. It follows the exact same structure, data flow, token usage and component rules (`components/admin/`, `lib/api/`, shared `components/common/` and `components/layout/`).
- A route's `page.js` is a Server Component that fetches data, handles `notFound()`, sets metadata and composes sections.
- Special files per route as needed: `layout.js`, `loading.js` (size-reserving skeleton), `error.js`, `not-found.js`.
- Route groups `(marketing)`, `(app)` may separate layouts without changing URLs; don't introduce abstraction unnecessarily.
- Dynamic segments `[slug]`; generate static params where possible.
- Route handlers `app/api/**/route.js` call `lib/api`; they contain no UI.
- Public URLs are a contract with users and search engines: **never change them without explicit approval**; moved URLs get permanent redirects.
- Private/admin routes: authenticated, `noindex`, excluded from sitemap. (Public routes must never accidentally be `noindex`.)
- No unnecessary route abstraction (no generic "page factory" routes).
