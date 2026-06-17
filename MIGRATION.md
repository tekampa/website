# Hugo Blox Migration

The production repository was migrated from the legacy Academic theme to the
Hugo Blox source prepared in `website_temp`.

## Current Structure

- Hugo Extended 0.136.5
- Hugo Blox Tailwind module
- Homepage content in `content/_index.md`
- Profile data in `content/authors/admin/_index.md`
- Site configuration in `config/_default/`
- Custom Columbia styling in `assets/css/`
- GitHub Pages deployment in `.github/workflows/publish.yaml`

## Removed

- Legacy Hugo configuration and widget content
- Bundled Academic theme and theme gitlink
- Generated `public` submodule
- Demo posts, publications, projects, and experience pages
- Netlify and Pagefind integration
- Source-controlled `CNAME`
- Unused images, layouts, workflows, and starter files

## Compatibility

Current downloads live under `static/uploads/`. Compatibility copies remain
under `static/files/` so links published by the previous website continue to
resolve.

The custom domain remains configured in GitHub Pages settings. The repository
does not contain a `CNAME` file.

## Production Cutover

### Before Merging

1. Fetch the latest remote state and rebase the migration branch.
2. Commit and push `migration/hugo-blox-production`.
3. In `tekampa/website`, open **Settings → Pages** and set **Source** to
   **GitHub Actions**.
4. Keep `waldotekampa.me` assigned to `tekampa/tekampa.github.io` until the
   new workflow has deployed successfully.

GitHub Pages must be enabled before merging. The workflow's default token
cannot enable Pages for a repository where Pages is currently disabled.

### Merge and Initial Deployment

1. Merge the migration branch into `master`.
2. Confirm that **Deploy website to GitHub Pages** succeeds.
3. Inspect the deployment at `https://tekampa.github.io/website/`.

The project URL is only a staging check. Homepage links use root paths for the
production custom domain, so PDF and navigation links are authoritative only
after the domain cutover.

### Move the Custom Domain

1. Remove `waldotekampa.me` from the Pages settings of
   `tekampa/tekampa.github.io`.
2. Add `waldotekampa.me` under **Settings → Pages → Custom domain** in
   `tekampa/website`.
3. Do not change the existing DNS records.
4. Manually rerun the deployment workflow so Hugo rebuilds with
   `https://waldotekampa.me/` as the Pages base URL.
5. Enable **Enforce HTTPS** when GitHub makes the option available.

### Verify

1. Confirm `https://waldotekampa.me/` serves the new homepage.
2. Confirm `https://www.waldotekampa.me/` redirects to the apex domain.
3. Test all homepage section links.
4. Test the CV and paper downloads under `/uploads/`.
5. Test the compatibility downloads under `/files/`.
6. Confirm canonical, Open Graph, RSS, robots, and sitemap URLs use
   `https://waldotekampa.me/`.

### Rollback

If the new deployment fails after the domain move:

1. Remove the custom domain from `tekampa/website`.
2. Reassign `waldotekampa.me` to `tekampa/tekampa.github.io`.
3. Leave DNS unchanged.
4. Revert the migration merge on `master` if further source changes are
   required.

Keep `tekampa/tekampa.github.io` unchanged until the new deployment has been
stable for several days.

## Verification

```bash
asdf plugin add hugo
asdf install hugo extended_0.136.5
go mod download
asdf exec hugo --gc --minify
```

The local Hugo version should match `.tool-versions` and the GitHub Actions
workflow: Hugo Extended 0.136.5.

The deployment workflow runs when changes are pushed to `master`.
