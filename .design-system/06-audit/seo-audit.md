# SEO audit

### Metadata
- **Expected:** unique title (<= ~60 chars) and description (120-160) per page.
- **Common problems:** duplicate/missing titles, template not applied.
- **How to debug:** view-source; fetch the page HTML and inspect `<title>` and meta tags.
- **How to fix:** set metadata per page through the project's shared metadata helper.

### Canonical, robots, indexability
- **Expected:** canonical = final public URL; index/follow on public pages; sitemap and robots.txt present and accurate.
- **Common problems:** accidental `noindex` (staging leftovers, metadata, `X-Robots-Tag`), wrong canonical host, sitemap missing dynamic slugs, blocked assets.
- **How to debug:** check `<meta name="robots">` and response headers; `/robots.txt`; `/sitemap.xml`; Search Console URL inspection.
- **How to fix:** remove stray `noindex`; env-driven site URL; generate sitemap from the data layer.

### Open Graph / Twitter
- **Expected:** title, description, url, image (1200x630), card type.
- **How to debug:** social-card validators; view-source.
- **How to fix:** add via shared metadata helper.

### Structured data
- **Expected:** valid JSON-LD matching visible content.
- **Common problems:** invalid or mismatched data.
- **How to debug:** Rich Results Test / schema validator.
- **How to fix:** generate from real page data in a Server Component.

### Content structure and links
- **Expected:** one `h1`; logical heading order; descriptive link text; internal links between related pages; image alt; fast Core Web Vitals.
- **Common problems:** missing/duplicate `h1`, "read more" links, orphan pages, redirect chains.
- **How to fix:** restructure headings; improve anchors; add internal links; collapse redirects.

### URL safety
- **Expected:** public URLs unchanged without explicit approval; moved URLs permanently redirected.
