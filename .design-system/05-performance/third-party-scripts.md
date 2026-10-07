# Third-party scripts

Analytics, tag managers, chat widgets, CAPTCHA, heatmaps, social embeds, marketing pixels. They hurt LCP, INP and TBT and are usually the biggest avoidable cost.

## Rules

- **Not global by default.** Don't put them in the root layout unless every page truly needs them. Load only on the routes/components that need them (CAPTCHA only on the form page; chat only on support pages).
- Load via `next/script` with an appropriate strategy:
  - `lazyOnload`: chat widgets, heatmaps, social, marketing (idle time)
  - `afterInteractive`: analytics that must run early
  - `worker` (experimental): offload where supported
  - `beforeInteractive`: almost never
- Never block the critical path: no synchronous `<script src>` in `<head>`; no marketing tag before LCP.
- Facade pattern for heavy embeds (video, maps, chat): static image/button first; load the real embed on click/visibility/intent. Reserve its size (no CLS).
- Consent: don't load tracking before consent where required.
- Prefer lightweight/first-party or server-side options. Review each script's cost (size, long tasks, requests) before adding; document owner and purpose.
- Use the framework's official third-party wrappers where they fit.
- Audit regularly: Network (filter third-party), Performance (attribute long tasks), Lighthouse third-party insight. Remove what nobody uses.

```jsx
// documentation snippet: only on the page that needs it
import Script from "next/script";
<Script src="https://example.com/captcha.js" strategy="lazyOnload" />
```
