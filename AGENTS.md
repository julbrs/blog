# Agent Notes

## Fast commands
- Use `pnpm` (lockfile is `pnpm-lock.yaml`).
- Dev server: `pnpm dev`.
- Production build: `pnpm build`.
- Preview built site: `pnpm preview`.
- There is no dedicated lint/test script; for Astro + content/type checks use `pnpm astro check`.

## Project shape
- Single Astro site (no monorepo).
- Base layout stack: `src/layouts/LayoutBase.astro` -> `src/layouts/Layout.astro` -> page content.
- Global styles are loaded from `src/styles/global.css` via `LayoutBase`; avoid re-importing globally elsewhere.
- Path alias `@/*` maps to `src/*` in `tsconfig.json`.

## Content and routing gotchas
- Content collections are defined in `src/content.config.ts`: `blog`, `outdoor`, `recipe` (note singular `recipe`).
- `blog` entries require `postSlug` and are routed by `postSlug` via `src/pages/[slug].astro`.
- `outdoor` and `recipe` pages are routed by `post.id` via `src/pages/outdoor/[slug].astro` and `src/pages/recipes/[slug].astro`.
- If you change slug behavior, update both `getStaticPaths()` and list links (`src/pages/blog/index.astro`, `src/pages/outdoor/index.astro`, `src/pages/recipes/index.astro`).

## Markdown/content specifics
- Markdown alert syntax (`> [!NOTE]`, etc.) is enabled through `remark-github-blockquote-alert` in `astro.config.mjs`.
- Alert styling is imported in `src/layouts/Layout.astro` (`remark-github-blockquote-alert/alert.css`); keep this if alerts are used.
- `heroImage` in `outdoor`/`recipe` frontmatter uses Astro image metadata (`image()` schema), so use local relative file paths.

## Tooling and deploy
- Tailwind is configured with the Vite plugin (`@tailwindcss/vite`) and `@import "tailwindcss"` in `src/styles/global.css` (no `tailwind.config.*` file).
- GitHub Pages deploy runs from `.github/workflows/deploy.yml` on push to `main` using `withastro/action@v3` with pnpm.
- `LayoutBase` injects GoatCounter only in production (`import.meta.env.MODE === "production"`); preserve this guard when editing analytics.
