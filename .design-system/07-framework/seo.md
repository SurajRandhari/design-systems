# SEO contract

Every public page has:

| Item | Standard |
|---|---|
| Title | Unique, <= ~60 chars, brand suffix via template |
| Description | Unique, 120-160 chars |
| Canonical | Absolute URL of the final public page |
| Robots | index/follow on public pages; `noindex` only on private/admin/utility pages, deliberately |
| Open Graph | title, description, url, site name, image 1200x630 |
| Twitter | `summary_large_image` card with title, description, image |
| Structured data | JSON-LD for the page type (Organization, WebSite, BreadcrumbList, Article, Product, FAQ), matching visible content |
| Sitemap | Includes all public routes, including dynamic slugs; excludes private routes |
| robots.txt | Allows crawling of public content, references the sitemap |
| Headings | One `h1`; logical `h2-h3`; semantic HTML |
| Internal linking | Related pages link to each other with descriptive anchor text |
| Images | Meaningful `alt`; dimensions set |
| Performance | Core Web Vitals are a ranking factor; follow `../05-performance/` |

## Rules

- Do not accidentally introduce `noindex` (check metadata and `X-Robots-Tag` headers, especially after copying from staging).
- Do not change public URLs without explicit approval; moved URLs need permanent redirects.
- Build metadata through one shared per-project helper so every page is consistent; the helper is project code, not part of this repository.
- Structured data must be generated from real page data, never hand-copied.
- Audit with `../06-audit/seo-audit.md`.
