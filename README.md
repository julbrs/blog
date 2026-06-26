# Sidoine.org

Personal Astro site for blog posts, outdoor adventure journals, and outdoor recipes.

## Stack

- [Astro 5](https://astro.build/) static site
- Tailwind CSS v4 via `@tailwindcss/vite`
- Astro Content Collections (`blog`, `outdoor`, `recipe`)
- Markdown callout support with `remark-github-blockquote-alert`

## Quick start

Requirements:

- Node.js 20+
- pnpm

Install dependencies:

```bash
pnpm install
```

Run locally:

```bash
pnpm dev
```

Build production output:

```bash
pnpm build
```

Preview the build:

```bash
pnpm preview
```

Run Astro/content/type checks:

```bash
pnpm astro check
```

## Content model and routes

Collections are defined in `src/content.config.ts`:

- `blog`: markdown/mdx entries under `src/content/blog`
- `outdoor`: markdown/mdx entries under `src/content/outdoor`
- `recipe`: markdown/mdx entries under `src/content/recipes`

Routing:

- Blog posts use frontmatter `postSlug` and render at `/${postSlug}/` (`src/pages/[slug].astro`)
- Outdoor entries use `post.id` and render at `/outdoor/${post.id}/`
- Recipe entries use `post.id` and render at `/recipes/${post.id}/`

If you change slug logic, update both route pages and list pages.

## Project structure

```text
src/
  components/      Shared UI components
  content/         Markdown/MDX content and media assets
  layouts/         Base and section layouts
  pages/           Astro page routes
  styles/          Global stylesheet (`global.css`)
```

Layout composition:

- `LayoutBase.astro`: HTML shell, global CSS import, production analytics snippet
- `Layout.astro`: wraps pages with header/footer and imports alert styles
- Page files: render collection content and section-specific UI

## Styling notes

- Global styles are loaded from `src/styles/global.css`
- Tailwind is configured in `astro.config.mjs` with the Vite plugin (no `tailwind.config.*`)
- Path alias `@/*` maps to `src/*` in `tsconfig.json`

## Deployment

GitHub Pages deploy is configured in `.github/workflows/deploy.yml`:

- Trigger: push to `main`
- Build/deploy action: `withastro/action@v3`
- Package manager: pnpm

## Notes

- GoatCounter analytics is injected only in production mode (`LayoutBase.astro`).
- Markdown callouts like `> [!NOTE]` are enabled through the remark plugin and alert CSS import.
