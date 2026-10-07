# Page example (documentation snippet, not runnable)

Illustrates the contract for a dynamic product page: Server Page -> Server Sections -> data via `lib/api`.

```jsx
// app/products/[slug]/page.js
import { notFound } from "next/navigation";
import { getProductBySlug, getRelatedProducts } from "@/lib/api/products";
import HeroSection from "@/components/products/HeroSection";
import FeaturesSection from "@/components/products/FeaturesSection";
import RelatedSection from "@/components/products/RelatedSection";

export async function generateMetadata({ params }) {
  const { slug } = await params;
  const product = await getProductBySlug(slug);
  return product ? { title: product.name, description: product.summary /* + canonical, OG, Twitter */ } : {};
}

export default async function ProductPage({ params }) {
  const { slug } = await params;
  const product = await getProductBySlug(slug);
  if (!product) notFound();
  const related = await getRelatedProducts(product.id);   // independent calls -> Promise.all

  return (
    <>
      <HeroSection product={product} />            {/* likely LCP element: the only `priority` image */}
      <FeaturesSection features={product.features} />
      <RelatedSection products={related} />
    </>
  );
}
```

## Contract checks for this page
- LCP element identified and recorded (hero image).
- `loading.js` skeleton reserves final sizes; `not-found.js` exists.
- One `h1` (inside `HeroSection`); metadata, canonical, sitemap entry.
- Verified at 320 - 1920; audited per `../06-audit/`.
- The same pattern applies to `app/admin/users/page.js` (with `components/admin/*` sections).
