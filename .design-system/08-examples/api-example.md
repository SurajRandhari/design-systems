# API-layer example (documentation snippet, not runnable)

```js
// lib/api/products.js   (server-only module)
export async function getProductBySlug(slug) {
  const { data, error } = await db.from("products").select("id,slug,name,summary,image_url").eq("slug", slug).maybeSingle();
  if (error) throw new Error(`getProductBySlug failed: ${error.message}`);
  return data ? { id: data.id, slug: data.slug, name: data.name, summary: data.summary, image: data.image_url } : null;
}
```

```js
// fetch variant with cache policy beside the call
const res = await fetch(`${process.env.API_URL}/posts?limit=12`, { next: { revalidate: 3600, tags: ["posts"] } });
if (!res.ok) throw new Error(`getPosts failed: ${res.status}`);
```

Points: selects only needed fields; maps to a UI shape once; `null` for not-found, throw for failure; limit on lists; cache policy next to the fetch; no UI imports; components never import the DB client.
