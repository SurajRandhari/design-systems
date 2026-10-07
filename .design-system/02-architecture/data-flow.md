# Data flow contract

```
Database / External API
        ↓
lib/api
        ↓
Server Component
        ↓
Page
        ↓
Section
        ↓
Reusable Component
        ↓
UI Primitive
```

Presentation components (Section and below) receive plain props. They never fetch, never query a DB, never read secrets. Example of what is forbidden: `<ProductCard />` calling `supabase.from(...)`; the page fetches and passes props.

## Server fetching
Fetch in Server Components (pages/sections/layouts) through `lib/api`. Default choice for all read data.

## Client fetching
Only for data that is user-specific, live, or driven by client interaction (search-as-you-type, polling, infinite scroll). Use a small Client Island with a fetching library or Route Handler. Never fetch in `useEffect` what the server could deliver.

## Mutations
Server Actions or Route Handlers that call `lib/api`. Validate on the server. After success, revalidate the affected paths/tags. Show pending state; keep the UI responsive (optimistic UI only when failure is cheap to roll back).

## Caching
Static rendering/ISR for public content. Dynamic (`no-store`) only for per-user or real-time data. Declare cache policy beside the fetch. Using dynamic APIs (cookies, headers, searchParams) makes a route dynamic; do so deliberately.

## Revalidation
Time-based (`revalidate`) for content that changes occasionally; on-demand (path/tag) after mutations or CMS webhooks. Tag consistently per resource.

## Loading states
`loading.js` and `<Suspense>` boundaries with skeletons that **reserve the final size** (no layout shift). Stream slow, non-critical sections.

## Error states
`error.js` per route segment for unexpected failures; `not-found.js` for `null` results; inline error UI for recoverable section-level failures. Messages are human-readable and accessible (announced to assistive tech).

## Empty states
Every list/collection component defines an empty state (explanation + next action). Design it before wiring data.

## Request waterfalls
Don't `await` independent requests sequentially. Start them together (`Promise.all`) or stream via Suspense. Avoid fetching in nested children when the parent can fetch in parallel. Waterfalls hurt TTFB and LCP.

## Parallel requests
```js
const [product, reviews] = await Promise.all([getProduct(slug), getReviews(slug)]);
```
(documentation snippet; not runnable.)
