# AI coding-agent contract

Read `../DESIGN-SYSTEM-RULES.md` first. This file defines how an agent must behave in any project that adopts this design system.

## Operating rules

1. **Inspect before changing.** Read `package.json`, framework/Tailwind config, global CSS, `components.json`, `app/`, `components/`, `lib/`, `hooks/`, `public/`. Report what you found and what you intend to change before significant changes.
2. **Preserve what works.** Don't blindly overwrite existing architecture. If something conflicts with the contract, document the conflict before changing it.
3. **Smallest change.** No unrelated edits, refactors, renames, dependency additions, or new abstractions.
4. **Tokens, not values.** Use semantic tokens; never raw colors, hex, palette names, or arbitrary px values. If a needed token is missing, propose adding it (name per `../01-design-tokens/token-architecture.md`); don't hardcode.
5. **Mobile-first, all tiers.** Every UI change must define and verify mobile, tablet, desktop and large desktop.
6. **Server by default.** Add `"use client"` only with a stated reason, at the smallest leaf.
7. **Measure, don't assume.** Establish a baseline before performance work; re-measure after.
8. **Never** change public URLs, delete working code, alter DB structure or business logic, or commit/push without explicit instruction.
9. **Verify.** Run lint and production build; run the relevant audits; report results honestly, including failures and anything skipped.

## Definition of done for any UI task

Desktop ✓ Tablet ✓ Mobile ✓ Keyboard ✓ Accessibility ✓ Loading/Empty/Error states ✓ Hover/Focus/Disabled ✓ Responsive type and spacing ✓ Images optimized ✓ No layout shift ✓ No unnecessary client JS ✓ Lint ✓ Build ✓

## What may vary per project (don't "fix" these across projects)
Brand colors, fonts, weights, exact type scale, shadow strength, radius values, content, component variants.

## What must be consistent (never deviate)
Token names/categories, folder and component architecture, data architecture and flow, naming, responsive method, accessibility and performance standards, audit method, these AI rules.

## When the contract and the project disagree
Stop and report: state the conflict, the options, and a recommendation. Don't silently pick one.

Decision answers: `decision-guide.md`.
