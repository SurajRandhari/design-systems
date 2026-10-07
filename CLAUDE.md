# CLAUDE.md

## Design System

This project follows our personal frontend design system.

Before making any frontend-related changes, read and follow these documents:

- `.design-system/DESIGN-SYSTEM-RULES.md`
- `.design-system/09-ai-rules/ai-agent-contract.md`
- `.design-system/09-ai-rules/decision-guide.md`

These documents are the source of truth for the project's frontend architecture and development conventions.

The design system must be followed for:

- Design tokens and semantic styling
- Colors, typography, spacing, shadows, radius, motion, z-index, and breakpoints
- Folder and component architecture
- Next.js App Router structure
- Data flow and API architecture
- Server vs Client Component decisions
- shadcn/ui usage
- Responsive behavior across mobile, tablet, desktop, and large desktop
- Accessibility
- SEO
- Core Web Vitals and frontend performance
- Component naming and organization
- Audit and debugging workflows
- AI/coding-agent decision making

### Required Rules

1. Read the three referenced design-system documents before making architectural or frontend implementation decisions.
2. Treat the design-system documentation as the project's frontend constitution.
3. Use semantic design tokens instead of hardcoded colors, arbitrary spacing, typography values, shadows, or other visual values.
4. Follow the documented folder structure and component architecture.
5. Keep Server Components as the default and use Client Components only when interactivity or browser APIs require them.
6. Follow the documented responsive contract. Mobile, tablet, desktop, and large desktop must all be considered.
7. Follow the documented accessibility, SEO, and performance requirements.
8. Before making significant changes, inspect the existing implementation and preserve working behavior.
9. Do not create new architectural patterns that conflict with the design system without first identifying and reporting the conflict.
10. If the project implementation conflicts with the design system, stop and explain the conflict before making a broad architectural change.
11. Do not change existing public URLs unless explicitly requested.
12. Do not create barrel `index.js` files unless explicitly requested.
13. Do not modify unrelated files or functionality.
14. Keep the implementation focused on the requested task.
15. Do not introduce unnecessary dependencies.
16. Validate the changes before committing.

### Git Commit and Push

After completing the requested work:

1. Run the appropriate validation checks for the project, including linting and a production build when applicable.
2. Review the final `git status`.
3. Review the changed files with `git diff --stat` and, when necessary, `git diff`.
4. Make sure there are no unrelated changes.
5. Stage only the files related to the requested task.
6. Create a clear, conventional commit message describing the actual change.
7. Commit the changes.
8. Confirm the commit was created successfully.
9. Push the commit to the `main` branch on the configured remote.
10. Confirm that the push completed successfully and that the local `main` branch is synchronized with the remote.
11. Report the final commit hash, commit message, branch, and push result.

### Important Git Safety Rules

- Do not use `git reset --hard`.
- Do not delete or overwrite unrelated user changes.
- Do not force-push.
- Do not amend an existing commit unless explicitly requested.
- Do not commit unrelated files.
- If the working tree contains unrelated user changes, preserve them and do not include them in the commit.
- If the current branch is not `main`, do not blindly switch branches if that could risk losing work. Inspect the repository state first and report the situation.
- If merging, rebasing, conflicts, or other unexpected Git conditions occur, stop and report them rather than making destructive decisions.
- Push to `main` only after validation passes.

The goal is consistency: the project may have its own branding, content, data, and implementation details, but its frontend architecture and development methodology must remain aligned with the personal design system.
