# Data architecture contract (`lib/`)

```
lib/
├── api/         data access
├── data/        static/configuration data
├── constants/   constants
├── config/      configuration
└── utils/       pure utilities
```

This design system defines the structure only; it implements no API.

| Folder | Holds | Examples |
|---|---|---|
| `lib/api/` | One module per resource. The ONLY layer that talks to a database or external API. | `products.js`, `users.js` |
| `lib/data/` | Static/config content consumed by Server Components | `navigation.js`, `faqs.js` |
| `lib/constants/` | Fixed values | `routes.js`, `site.js` |
| `lib/config/` | Environment-derived config, fonts, feature flags, client factories | `fonts.js`, `env.js` |
| `lib/utils/` | Pure, framework-free helpers | `formatDate.js`, `formatPrice.js`, `cn.js` |

## `lib/api` rules

- Each function: input -> fetch/DB -> **mapped plain object** -> return. Map backend field names to UI shapes once, here.
- Server-only: mark modules that use secrets or DB clients as server-only so they cannot be bundled into client code.
- Not found -> return `null` (page calls `notFound()`); unexpected failure -> throw (caught by `error.js`).
- Create clients once (in `lib/config` or a private module), not per call.
- Request only the fields the UI renders; paginate/limit every list query.
- Validate and sanitize all external input (route params, search params, form data).
- Cache policy lives next to the fetch (revalidate/tags), see `data-flow.md`.
- Components never import DB/API clients. UI work never changes DB schemas, endpoints or business logic.
- No repository/service/adapter layers unless there are two or more real backends.

## Other rules

- `lib/` contains no JSX and no React components.
- `lib/utils` functions are pure; no hidden I/O.
- Secrets only via server env vars; only `NEXT_PUBLIC_*` values are browser-visible.
