# Waldo Ojeda Website

Source for [waldotekampa.me](https://waldotekampa.me/), built with Hugo
0.136.5 and Hugo Blox.

## Local Development

Install Go and [asdf](https://asdf-vm.com/), then install the Hugo plugin and
the pinned Hugo Extended version used by GitHub Actions. A plain `asdf install`
will not install Hugo until the plugin is available, and `hugo latest` may not
match the deployment version.

```bash
asdf plugin add hugo
asdf install hugo extended_0.136.5
go mod download
```

Start the local development server:

```bash
asdf exec hugo server
```

Create a production build:

```bash
asdf exec hugo --gc --minify
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
