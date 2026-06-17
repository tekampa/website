# Waldo Ojeda Website

Source for [waldotekampa.me](https://waldotekampa.me/), built with Hugo
0.163.2 and Hugo Blox.

## Local Development

Install Go and Hugo Extended. On macOS, Hugo ships only a `.pkg` installer for
recent releases, so install it with [Homebrew](https://brew.sh/) to match the
version used by GitHub Actions:

```bash
brew install hugo   # or: brew upgrade hugo
go mod download
```

Confirm the version matches the deployment version (`HUGO_VERSION` in
`.github/workflows/publish.yaml`):

```bash
hugo version   # expect: hugo v0.163.2+extended ...
```

Start the local development server:

```bash
hugo server
```

Create a production build:

```bash
hugo --gc --minify
```

The generated `public/` directory is ignored because GitHub Actions builds the
site from source.

## Content

- Homepage sections: `content/_index.md`
- Biography, interests, education, and social links:
  `content/authors/admin/_index.md`
- Navigation: `config/_default/menus.yaml`
- Site configuration: `config/_default/`
- Custom styles: `assets/css/custom.css`
- CV and paper downloads: `static/uploads/`

Compatibility copies remain under `static/files/` so links from the previous
website continue to work.

## Deployment

Pushing to `master` runs `.github/workflows/publish.yaml`, which builds the
site and deploys it through GitHub Pages.

To trigger a deploy manually (without a new commit), open the repository's
**Actions** tab, select the **Deploy website to GitHub Pages** workflow, and
click **Run workflow** on the `master` branch. You can also re-run the jobs of
a previous run from that run's page using **Re-run all jobs**.

The custom domain is managed in the repository's GitHub Pages settings. This
source intentionally does not include a `CNAME` file.
