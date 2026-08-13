# Index — documentation index generator

A single-page tool for building the index of a printed document. You type
entries and the pages they start on; it produces a paginated, print-ready
index. Everything runs in the browser — no account, no upload, no server.

## Features

- **Entries with page numbers** — add a title and its starting page; the list
  stays sorted by page.
- **Insert with page shifting** — insert an entry (or several consecutive
  pages' worth) at any position and later entries shift automatically.
- **Inline editing** — edit page numbers in place; delete entries; search to
  filter the list.
- **Live preview** — see the finished index, paginated, as you type.
- **Print** — a dedicated print stylesheet renders the index to paper or PDF.
- **Save and load** — export to JSON or CSV, and load either back in. Sample
  files are downloadable from the UI if you want to see the shapes.
- **Duplicate detection** — warns when a title is already in the index.
- **Keyboard support** — `Enter` to add an entry, `Ctrl` shortcuts, and a skip
  link to the preview.

Nothing is persisted between sessions. Save a JSON copy if you want to pick the
work up later.

## Usage

Open `index.html` in a browser. That's the whole app — there is no build step,
no dependency install, and no toolchain.

```
git clone <this repo>
cd indexer
xdg-open index.html   # or: open index.html
```

The page also works from `file://` with no network, though it will fall back to
system fonts (the Geist / Instrument Serif families load from Google Fonts when
online).

## File formats

### JSON

```json
{
  "title": "Meridian 400 Field Service Manual",
  "note": "Revised 14 March 2026. Supersedes revision C.",
  "entries": [
    { "title": "Safety notices", "page": 3 },
    { "title": "Unpacking and siting", "page": 11 }
  ],
  "exportDate": "2026-03-14T00:00:00.000Z"
}
```

`exportDate` is written on export and ignored on import.

### CSV

```csv
Document Title: Meridian 400 Field Service Manual
Note: Revised 14 March 2026. Supersedes revision C.

Title,Page
Safety notices,3
"Unpacking and siting",11
```

The two header lines are only emitted when a note is set; a bare `Title,Page`
file loads fine. Titles containing commas or quotes are quoted, with embedded
quotes doubled.

## Project layout

```
index.html            the entire application — markup, styles, and script
.github/workflows/    GitHub Pages deployment
plans/                advisory implementation plans (see plans/README.md)
LICENSE
```

`index.html` is deliberately a single file: no framework, no bundler, no
runtime dependencies. Keep it that way when making changes.

## Deployment

Pushes to `master` deploy the repository to GitHub Pages via
`.github/workflows/static.yml`.

## License

See [LICENSE](LICENSE).
