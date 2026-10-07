# Code quality audit

### Lint and build
- **Expected:** lint passes with no new warnings; production build succeeds.
- **Common problems:** disabled rules, ignored build errors, warnings normalized.
- **How to debug:** run the project's lint and production build scripts; read the full output.
- **How to fix:** fix the cause; don't suppress rules without a written reason.

### Simplicity
- **Expected:** no needless wrappers, hooks, context providers, state libraries, or utility dumps.
- **Common problems:** abstraction "for later", pass-through components, one-use hooks, giant `utils`.
- **How to debug:** for each abstraction ask: what concrete duplication or need does it remove today?
- **How to fix:** inline it; delete after verifying usage (grep).

### Duplication and consistency
- **Expected:** repeated UI promoted to `common/` once (not copy-pasted); repeated class strings extracted when 3+ uses.
- **How to debug:** search for near-identical components/class lists across page folders.
- **How to fix:** promote and re-import; keep naming conventions.

### Dependencies
- **Expected:** every dependency used, justified and size-checked.
- **How to debug:** dependency-usage tooling; bundle analyzer.
- **How to fix:** remove after confirming no usage; prefer platform features.

### Readability and safety
- **Expected:** clear names, small files, comments explain *why*; no secrets in the repo; inputs validated server-side; no `dangerouslySetInnerHTML` with unsanitized data; no `console.log` leftovers.
- **How to debug:** code review; secret scanning; grep.
- **How to fix:** refactor locally; rotate any exposed secret.

### Error handling and states
- **Expected:** loading, empty and error states exist for every data view; errors are handled at the right layer.
- **How to fix:** add `loading`/`error`/empty components per `../02-architecture/data-flow.md`.
