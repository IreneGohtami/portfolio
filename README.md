# Portfolio

A static, no-build portfolio site — plain HTML and CSS, no JavaScript, no CI. It
showcases seven projects, each with a demo video and a technology stack, and is
deployed via GitHub Pages straight from the `main` branch root. There is nothing
to install, transpile, or bundle: the files you see are the files that get served.

## Project structure

```
portfolio/
├── index.html                 # Single-page entry, served from the repo root
├── styles.css                 # Single stylesheet, light fixed theme
├── .nojekyll                  # Makes GitHub Pages serve files as-is (no Jekyll)
├── README.md                  # This file
└── assets/
    ├── tuinet-v2/{demo.mp4, thumbnail.jpg}
    ├── holiday/{demo.mp4, thumbnail.jpg}
    ├── gds-connector/{demo.mp4, thumbnail.jpg}
    ├── blinders/{demo.mp4, thumbnail.jpg}
    ├── virtual-economy/{demo.mp4, thumbnail.jpg}
    ├── pawtner/{demo.mp4, thumbnail.jpg}
    └── pacman/{demo.mp4, thumbnail.jpg}
```

Each project has its own `assets/<slug>/` folder holding a `demo.mp4` (the video)
and a `thumbnail.jpg` (the video poster). All references in `index.html` are
repository-relative, so the site works unchanged under a project subpath such as
`https://user.github.io/portfolio/`.

## Re-copying demo assets

The media under `assets/` is copied (and renamed) from each source project's
`brag-output/` directory. Re-run these steps whenever a `brag.mp4` is regenerated
and you want the portfolio to pick up the new video.

These commands assume the `portfolio` repo sits beside its source repos under the
same parent directory, so each source is reached with `../<source-dir>/`.

```sh
cd portfolio

# Ensure the destination folders exist
mkdir -p assets/tuinet-v2 assets/holiday assets/gds-connector \
         assets/blinders assets/virtual-economy assets/pawtner assets/pacman

# Copy and rename: brag.mp4 -> demo.mp4, brag.jpg -> thumbnail.jpg
cp ../tuinet-v2/brag-output/brag.mp4            assets/tuinet-v2/demo.mp4
cp ../tuinet-v2/brag-output/brag.jpg            assets/tuinet-v2/thumbnail.jpg
cp ../holiday-landing-page/brag-output/brag.mp4 assets/holiday/demo.mp4
cp ../holiday-landing-page/brag-output/brag.jpg assets/holiday/thumbnail.jpg
cp ../gds-mcp-web/brag-output/brag.mp4          assets/gds-connector/demo.mp4
cp ../gds-mcp-web/brag-output/brag.jpg          assets/gds-connector/thumbnail.jpg
cp ../blinders/brag-output/brag.mp4             assets/blinders/demo.mp4
cp ../blinders/brag-output/brag.jpg             assets/blinders/thumbnail.jpg
cp ../virtual-economy/brag-output/brag.mp4      assets/virtual-economy/demo.mp4
cp ../virtual-economy/brag-output/brag.jpg      assets/virtual-economy/thumbnail.jpg
cp ../pawtner/brag-output/brag.mp4              assets/pawtner/demo.mp4
cp ../pawtner/brag-output/brag.jpg              assets/pawtner/thumbnail.jpg
cp ../Pacman/brag-output/brag.mp4               assets/pacman/demo.mp4
cp ../Pacman/brag-output/brag.jpg               assets/pacman/thumbnail.jpg
```

Source → destination mapping:

| Source directory                     | Destination folder        | Rename                                       |
|--------------------------------------|---------------------------|----------------------------------------------|
| `../tuinet-v2/brag-output/`          | `assets/tuinet-v2/`       | `brag.mp4`→`demo.mp4`, `brag.jpg`→`thumbnail.jpg` |
| `../holiday-landing-page/brag-output/` | `assets/holiday/`       | `brag.mp4`→`demo.mp4`, `brag.jpg`→`thumbnail.jpg` |
| `../gds-mcp-web/brag-output/`        | `assets/gds-connector/`   | `brag.mp4`→`demo.mp4`, `brag.jpg`→`thumbnail.jpg` |
| `../blinders/brag-output/`           | `assets/blinders/`        | `brag.mp4`→`demo.mp4`, `brag.jpg`→`thumbnail.jpg` |
| `../virtual-economy/brag-output/`    | `assets/virtual-economy/` | `brag.mp4`→`demo.mp4`, `brag.jpg`→`thumbnail.jpg` |
| `../pawtner/brag-output/`            | `assets/pawtner/`         | `brag.mp4`→`demo.mp4`, `brag.jpg`→`thumbnail.jpg` |
| `../Pacman/brag-output/`             | `assets/pacman/`          | `brag.mp4`→`demo.mp4`, `brag.jpg`→`thumbnail.jpg` |

The copied files are committed to the repo so GitHub Pages serves them from the
same origin as the HTML. If a video is large enough to bump into GitHub's
file-size guidance, re-encode it at the `brag` step rather than adding anything
to the publishing pipeline here.

## GitHub Pages setup

This repo deploys as-is, with no build step:

1. In the repository, go to **Settings → Pages**.
2. Under **Source**, choose **Deploy from a branch**.
3. Set **Branch** to `main` and **Folder** to `/ (root)`.
4. Save. Pages publishes from the root, serving `index.html` directly.

The `.nojekyll` file at the root tells GitHub Pages to serve the files as-is and
skip Jekyll processing. Because every asset path in `index.html` is
repository-relative (no leading `/`), the site renders correctly under a project
subpath like `https://user.github.io/portfolio/`.

## Replace the placeholders before publishing

`index.html` ships with clearly marked bracketed placeholders, each tagged with a
`data-placeholder` attribute so they are easy to find. Search the file for
`data-placeholder` to locate every one, then replace:

- `[Your Name]` — appears in the `<title>`, the header name heading, and the
  footer copyright line.
- `[Professional Title]` — the subtitle under your name in the header.
- `[github-handle]` — inside the GitHub profile URL `https://github.com/[github-handle]`
  (header and footer).
- `[linkedin-handle]` — inside the LinkedIn URL
  `https://www.linkedin.com/in/[linkedin-handle]` (header and footer).
- `[you@example.com]` — inside the email link `mailto:[you@example.com]`
  (header and footer).

The site still renders with the placeholders in place; they are visibly bracketed
so it is obvious what remains to fill in before you publish.
