# Token example: same contract, two projects (documentation only)

```
Token (contract)        Project A (SaaS)                  Project B (Corporate)
--primary               #2563eb                           #059669
--primary-hover         darker step of primary            darker step of primary
--primary-foreground    #ffffff                           #ffffff
--background            #ffffff                           #fafaf9
--foreground            #0f172a                           #1c1917
--font-h1               clamp(2.5rem, 4vw, 4rem)          clamp(2.25rem, 3.5vw, 3.5rem)
--font-family-primary   "Inter"                           "Source Sans 3"
--radius-md             0.5rem                            0.125rem
--shadow-md             soft, layered                     minimal
```

Both projects' components use identical classes:

```
<button class="bg-primary text-primary-foreground hover:bg-primary-hover rounded-md text-button shadow-sm">
<h1 class="text-h1 text-heading">
```

Primitives -> semantic mapping, per project (names of primitives are the project's own):

```
palette-brand-600: #2563eb      ->   --primary: palette-brand-600
palette-brand-700: #1d4ed8      ->   --primary-hover: palette-brand-700
```

Re-brand = change those mappings/values; no component edits.
