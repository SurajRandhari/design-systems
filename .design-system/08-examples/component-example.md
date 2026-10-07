# Component example (documentation snippet, not runnable)

A page-specific Server Component: mobile-first, semantic tokens only, semantic HTML, sized image, no data access.

```jsx
// components/products/HeroSection.jsx
import Image from "next/image";
import PrimaryButton from "@/components/common/Buttons/PrimaryButton";

export default function HeroSection({ product }) {
  return (
    <section aria-labelledby="hero-title" className="bg-background py-section">
      <div className="container-page grid items-center gap-gap lg:grid-cols-2">
        {/* Mobile: stacked, text first, full-width CTA. lg: two columns. */}
        <div className="space-y-stack">
          <h1 id="hero-title" className="text-h1 text-heading">{product.name}</h1>
          <p className="text-body-lg text-foreground-secondary">{product.summary}</p>
          <PrimaryButton href={`/products/${product.slug}/buy`} className="w-full sm:w-auto">Get started</PrimaryButton>
        </div>
        <Image
          src={product.image} alt={product.imageAlt}
          width={1200} height={900} priority
          sizes="(min-width: 1024px) 50vw, 100vw"
          className="aspect-[4/3] w-full rounded-2xl object-cover shadow-lg"
        />
      </div>
    </section>
  );
}
```

## Why it conforms
- Colors/type/spacing/radius/shadow are semantic tokens (`bg-background`, `text-h1`, `gap-gap`, `rounded-2xl`, `shadow-lg`); no raw values.
- Mobile base, enhancement at `sm:` and `lg:`; content capped by the container utility.
- Heading tied to its section; image has reserved space and a `sizes` hint; one `priority` image.
- Server Component; no `"use client"`, no fetching; states (loading/empty/error) are handled by the page/route.
