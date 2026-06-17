# CLAUDE.md

Guidance for working in this repository.

## What this is

Source for [waldotekampa.me](https://waldotekampa.me/) — the personal academic
site of Waldo Ojeda. It is a static [Hugo](https://gohugo.io/) site built on the
[Hugo Blox](https://hugoblox.com/) `blox-tailwind` module (academic-cv starter).
There is no application code; everything is content (Markdown) and configuration
(YAML).

## Toolchain

- **Hugo Extended 0.163.2** — pinned in two places that must stay in sync:
  `hugoblox.yaml` and `.github/workflows/publish.yaml` (`HUGO_VERSION`).
  Change both together.
- **Go 1.19+** — Hugo Modules pull the theme; see `go.mod` / `go.sum`.
- **Homebrew** — used for local installs. Recent Hugo releases ship macOS only
  as a `.pkg`, so install the matching Extended build with `brew install hugo`
  (`brew upgrade hugo` to update) and confirm with `hugo version`.

## Common commands

```bash
# One-time setup
brew install hugo   # Hugo Extended; brew upgrade hugo to update
go mod download

# Local dev server (http://localhost:1313)
hugo server

# Production build (output in public/, which is gitignored)
hugo --gc --minify
```

## Layout

- `content/_index.md` — homepage; an ordered list of Hugo Blox blocks. Each
  block has an `id` that the nav links to via `/#<id>`.
- `content/authors/admin/_index.md` — profile: bio, interests, education,
  social links, avatar (`avatar.jpg`).
- `content/post/` — blog posts.
- `config/_default/` — site config:
  - `hugo.yaml` — core Hugo settings (baseURL, outputs, markup, taxonomies).
  - `params.yaml` — appearance, SEO, header/footer, features.
  - `menus.yaml` — top navigation. Link names map to homepage block `id`s.
  - `module.yaml` — Hugo Module imports and mounts (the theme).
  - `languages.yaml` — language setup (English only).
- `assets/css/` — custom Columbia-themed styling (`custom.css`, `themes/`).
- `static/uploads/` — current CV and paper PDFs.
- `static/files/` — compatibility copies so links from the previous (Academic
  theme) site still resolve. Do not delete without checking inbound links.

## Editing conventions

- **Nav and homepage stay in sync.** When you add, remove, or rename a homepage
  block in `content/_index.md`, update the matching entry in
  `config/_default/menus.yaml` (the URL is `/#<block-id>`). Current IDs: `about`,
  `workingpapers`, `worksinprogress`, `teaching`, `posts`, `contact`.
- **Use root-relative paths** for links and PDFs (e.g. `/uploads/cv.pdf`). The
  production base URL is the custom domain; relative-to-root keeps links correct
  there and avoids the GitHub Pages project-path staging URL.
- This is content, not code — there are no tests. Verify changes by running
  `hugo server` and viewing the affected page.

## Deployment

Pushing to `master` triggers `.github/workflows/publish.yaml`, which builds with
Hugo and deploys to GitHub Pages (Pages **Source** is set to **GitHub Actions**).
Manual deploys: **Actions** tab → **Deploy website to GitHub Pages** →
**Run workflow** on `master`.

The custom domain is configured in GitHub Pages settings; this repo
intentionally has **no `CNAME` file**. `public/` is gitignored — CI builds from
source.

See `README.md` for the developer-facing summary and `MIGRATION.md` for the
historical record of the Academic-theme → Hugo Blox cutover.
