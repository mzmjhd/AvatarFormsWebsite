# AvatarFormsWebsite

Website for the COMP0016 System Engineering Project: AvatarForms.

## Tech Stack

- HTML pages with shared component injection (`fetch` + partial HTML files)
- Tailwind CSS v4 (via CDN): `@tailwindcss/browser`
- Flowbite v4 (via CDN) for responsive/navigation behaviors
- Custom theme and dark-mode tokens in `css/styles.css`

## Project Structure

- `index.html`, `requirements.html`, `appendices.html`: pages
- `components/navbar.html`: top navigation + dark mode toggle
- `components/sidebar.html`: left sidebar navigation
- `components/breadcrumbs.html`: base breadcrumb root (`Home`)
- `css/styles.css`: theme variables, dark mode, typography, sidebar styles
- `.vscode/html.code-snippets`: developer snippets (including `afhtml`)

## Run Locally

Use a local server. Do not open pages directly with `file://` URLs, because component `fetch(...)` calls will fail.

Recommended options:

- VS Code Live Server extension
- Python: `python -m http.server 5500`

Then open `http://localhost:5500`.

## Developer Boilerplate (`afhtml`)

Use the VS Code snippet prefix `afhtml` (defined in `.vscode/html.code-snippets`) to scaffold a new page with:

- Required imports (Tailwind CDN, Flowbite CSS/JS, `css/styles.css`)
- Shared layout containers (`navbar-container`, `sidebar-container`, `breadcrumbs-container`)
- Default page layout (`min-h-screen`, fixed sidebar + main content)
- Shared script to load navbar/sidebar/breadcrumb components
- Breadcrumb generation helper (`breadcrumbPaths` + `addCurrentBreadcrumb()`)

### New Page Checklist (after using `afhtml`)

1. Save page as `<name>.html` at project root.
2. Set the `<title>` and page content placeholder.
3. Add an entry for your new page in the `breadcrumbPaths` object in that page.
4. Add navigation links in `components/navbar.html` and/or `components/sidebar.html` if needed.
5. Test in both light and dark mode.

## Tailwind + Flowbite Conventions

- Keep utility classes in markup for layout/spacing.
- Keep cross-page theme behavior in `css/styles.css` (tokens and shared rules).
- Flowbite components rely on including both:
	- Flowbite CSS in `<head>`
	- Flowbite JS before `</body>`
- Prefer existing classes/tokens already used in the project (`text-body`, `text-heading`, `rounded-base`, etc.).

## Dark Mode

- Dark mode is toggled by adding/removing `.dark` on `document.documentElement` (in `components/navbar.html`).
- Theme variables are defined in `css/styles.css` under `:root` and `.dark`.
- Global page background/text are handled at `html, body` level.
- Sidebar colors/hover states are controlled via sidebar-specific variables in `css/styles.css`.

## Common Gotchas

- If navbar/sidebar/breadcrumbs do not appear, check that you are running from a local server (not `file://`).
- If a new page has no breadcrumb label, add it to that page's `breadcrumbPaths` object.
- If dark mode looks inconsistent, move color logic to `css/styles.css` variables instead of ad-hoc per-page colors.

## Contribution Notes

- Reuse shared components where possible instead of duplicating nav/sidebar markup.
- Keep edits minimal and consistent with existing style tokens.
- Prefer updating `afhtml` snippet when layout conventions change, so new pages stay aligned.
