# Admin panel / dashboard contract

Admin panels, dashboards, SaaS apps and internal tools use the **same architecture** as marketing sites. No parallel structure.

| Concern | Location |
|---|---|
| Routes | `app/admin/**` (`page.js`, `users/page.js`, `settings/page.js`, `reports/page.js`) |
| Admin-specific components | `components/admin/` |
| Components reusable beyond admin | `components/common/` |
| Admin shell (sidebar, topbar) | `components/layout/` (or `components/admin/` if admin-only) |
| shadcn primitives (tables, dialogs, forms) | `components/ui/` |
| Data access | `lib/api/` |
| Nav config, column definitions | `lib/data/` |

## Rules

- Same tokens, same naming, same data flow (`lib/api` -> Server Component -> Page -> Section -> Component -> primitive).
- Admin is **not exempt** from responsive, accessibility or performance standards. Tables and dashboards must work on mobile (scroll wrapper or stacked layout), keyboard-operable, and meet contrast.
- Data-heavy views: server-side pagination/filtering/sorting; never ship whole datasets to the client.
- Client islands for interactivity (filters, sortable tables, charts), not whole pages.
- Dense UIs still keep 44px touch targets on touch devices; density options may adjust spacing tokens, not break the contract.
- Auth guard in the admin layout; admin routes are `noindex` and excluded from the sitemap.
- Loading, empty, error and permission-denied states are required for every data view.
- Destructive actions: confirmation dialog, clear labels, undo where feasible.
