# AGENTS.md

## Big Picture
- This repo is a single-page static site for GitHub Pages: all UI, styles, and behavior live in `index.html`.
- `CNAME` defines the production custom domain (`jelonsoftware.com`), so deploy assumptions should remain GitHub Pages compatible.
- There is no backend, package manager, or build step in the repository.

## Architecture and Data Flow
- `index.html` contains three layers in one file:
  - semantic HTML structure (hero area + events section)
  - inline CSS (theme variables, layout, responsive rules)
  - small inline JavaScript (DOM update for event count)
- Event data is authored directly in the events table markup (`<tbody>` rows in `index.html`), then JS derives a footer count from those rows.
- The inline SVG in `index.html` is part of page content (not an external asset), with accessibility metadata (`aria-labelledby`, `<title>`, `<desc>`).

## Project Conventions (Observed)
- Theme and color system is centralized with CSS custom properties in `:root` (for example `--bg`, `--ink`, `--accent`, `--panel`, `--shadow`).
- Responsive sizing uses CSS `clamp(...)` and media queries in the same stylesheet block.
- Styling favors simple utility-like class blocks (`.hero`, `.events`, etc.) rather than external component files.
- JavaScript is intentionally minimal and framework-free; keep behavior small and DOM-centric.

## Developer Workflow
- Primary edit surface: `index.html`.
- Domain config changes: `CNAME`.
- Project description/context: `README.md`.
- Since no build/test scripts are defined in-repo, validation is manual: open the page in a browser and verify layout, SVG rendering, and event-count behavior.

## Change Guidance for Agents
- Prefer surgical edits in `index.html`; avoid introducing tooling (bundlers/frameworks) unless explicitly requested.
- For visual/theme updates, modify `:root` variables first before changing individual rules.
- For event schedule updates, edit table rows and confirm the JS-driven count still matches row count.
- Preserve semantic/accessibility patterns already present in markup, especially SVG labels and section structure.
- Keep external dependencies at zero unless a task explicitly requires them.

