# Repository guidance

## Deployment warning

- The `main` branch is deployed on Cloudflare.
- **Do not push anything to any remote or branch unless the user explicitly instructs you to push.** Requests to edit, test, or commit do not authorize a push.
- Keep work local and do not trigger a deployment unless the user explicitly requests it.
- The README contains upstream template instructions for GitHub Pages; the user's Cloudflare setup and this warning take precedence.

## Project basics

- This is a Hugo academic website using the PaperMod theme in `themes/PaperMod/`.
- `config.yml` contains site configuration.
- `content/` contains page content; `static/` contains files served directly.
- `layouts/` contains template overrides, `assets/css/` contains styles, and `archetypes/` contains content templates.
- Run `hugo server` for a local preview at `http://localhost:1313/` and `hugo` to build the site locally.

## Working conventions

- Keep changes focused on the user's request and follow existing conventions.
- Prefer site-level templates and styles over edits to the bundled theme.
- For content, template, or style changes, check the local Hugo build and preview when available. Documentation-only changes do not require a build.

## Permanent paper links

Paper links live in `content/links/` and use the standalone template in
`layouts/links/single.html`. They build to ordinary HTML and need no hosting-specific
redirect rules or JavaScript. They are excluded from normal paper lists and feeds.
The front matter `url` places them under `/papers/` while keeping their source
files separate from the site's regular paper pages.

The demo at `/papers/2608.12211-bh_spin/` redirects to
https://arxiv.org/abs/2608.12211. Preview it with `hugo server`, then open
http://localhost:1313/papers/2608.12211-bh_spin/ directly.

To add a paper, create `content/links/your-short-slug.md`:

```yaml
---
title: "Your paper title"
url: "/papers/your-short-slug/"
status: "In preparation"
redirect_to: ""
---
```

An empty or omitted `redirect_to` displays the title and status (defaulting to
"Coming soon"). Optional Markdown below the front matter appears on the placeholder.
Do not mark unpublished papers as drafts: their placeholder must be built.

When the paper is available, set `redirect_to` to its full HTTPS URL and update
`status`. To change the destination later, edit `redirect_to` again. Keep the
`url` unchanged once shared, even if the title or filename changes. Use a unique
path and do not also create a page at that path in `static/` or elsewhere.

The redirect uses immediate HTML meta-refresh with a visible fallback link, not
an HTTP 301. Normal host/browser caching can still delay updates. The same HTML
works on any static host serving directory `index.html` files; keep your custom
domain when migrating hosts to preserve already-shared URLs.

To check the placeholder locally, temporarily clear the demo's `redirect_to`
and set `status: "In preparation"`, then reload the same local URL. Restore the
destination to check the redirect. Run `hugo --minify` to verify the build.
All work stays local until a push or deployment is explicitly requested.
