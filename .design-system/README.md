# Personal Frontend Design System: the Contract

This repository is a **documentation-only constitution** for every future frontend project (marketing sites, corporate sites, SaaS apps, admin panels, dashboards, internal tools, e-commerce). It contains rules, contracts, token definitions, audit methodology and AI-agent instructions. It contains **no application, no starter, no framework code**. Projects implement it elsewhere.

```
        DESIGN SYSTEM  (this repo: the contract)
              │
   ┌──────────┼──────────┬──────────┐
 Project A  Project B  Project C  Project D   (each: its own values & features)
```

## What varies vs. what is fixed

| MAY change per project | MUST stay consistent |
|---|---|
| Brand colors | Token **names** and **categories** |
| Font family and weights | Folder architecture |
| Exact typography scale values | Component architecture |
| Shadow strength | Data architecture and data flow |
| Radius values | Naming conventions |
| Content, copy, imagery | Responsive methodology |
| Component variants | Accessibility standards |
| Business logic, features | Performance standards and budgets |
| | Audit methodology |
| | AI development rules |

## Map

| Folder | Contents |
|---|---|
| `DESIGN-SYSTEM-RULES.md` | The one-page rule set (read first; AI agents start here) |
| `01-design-tokens/` | Token architecture, naming contract, color, typography, spacing, shadows, radius, motion, z-index, breakpoints |
| `02-architecture/` | Universal folder structure, routing, data architecture, data flow, server/client, admin panels, naming |
| `03-components/` | Component architecture, rules, accessibility contract |
| `04-responsive/` | Responsive contract and per-component responsive patterns |
| `05-performance/` | Core Web Vitals, performance contract, budgets, images, fonts, JavaScript, third-party scripts |
| `06-audit/` | Audit checklist and per-discipline audits, debug workflow |
| `07-framework/` | Framework conventions: Next.js, Tailwind, shadcn/ui, SEO |
| `08-examples/` | Documentation-only snippets (illustrative; not runnable) |
| `09-ai-rules/` | AI coding-agent contract and decision guide |

## How to use it

1. **Starting a project:** read `DESIGN-SYSTEM-RULES.md`; create the folder structure from `02-architecture/folder-structure.md`; define your project's values for every token in `01-design-tokens/` (names fixed, values yours); wire tokens to Tailwind per `07-framework/tailwind.md`.
2. **With an AI agent:** point it at `DESIGN-SYSTEM-RULES.md` and `09-ai-rules/` (e.g. reference from the project's `CLAUDE.md`/`AGENTS.md`).
3. **Before shipping:** run `06-audit/audit-checklist.md`.
4. **Existing project:** audit against the contract, document conflicts, migrate incrementally, keep public URLs.

> The design system defines the contract. Each project defines its implementation.
