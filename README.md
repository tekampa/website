# Waldo Ojeda Website

Source for [waldotekampa.me](https://waldotekampa.me/), built with Hugo
0.136.5 and Hugo Blox.

## Local Development

Install Go and [asdf](https://asdf-vm.com/), then install the pinned Hugo
version and download the Hugo modules:

```bash
asdf install
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

The custom domain is managed in the repository's GitHub Pages settings. This
source intentionally does not include a `CNAME` file.
