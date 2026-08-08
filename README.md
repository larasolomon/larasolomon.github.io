# larasolomon.com.au

Personal website for Lara Solomon, served as a static site from GitHub Pages at
<https://larasolomon.com.au/>.

## Files

| File | Purpose |
|---|---|
| `index.html` | Home page. No JavaScript anywhere on this site; light/dark aware. Includes schema.org JSON-LD. |
| `about/index.html` | Full biography, plus the "Which Lara Solomon is this?" question-and-answer section. |
| `oeis/index.html` | The mathematics in detail — term table, the three OEIS contributions, the checking identity. |
| `style.css` | Shared stylesheet. Extracted from the original inline `<style>` when the site grew past one page. |
| `index.md` | Plain-Markdown mirror of the home page, for text-only readers and LLM crawlers. |
| `llms.txt` | Structured summary for language models ([llmstxt.org](https://llmstxt.org/) convention). |
| `robots.txt` | Explicitly allows every search and AI crawler by name. |
| `sitemap.xml` | Sitemap covering the three HTML pages. |
| `<hex>.txt` | IndexNow key file — lets Bing/Copilot be pinged when a page changes. Filename is the key. |
| `favicon.svg` | LS monogram, browser tab icon. |
| `apple-touch-icon.png` | 180×180 square icon for iOS home-screen bookmarks. |
| `og-image.png` | 1200×630 share card used by `og:image` / `twitter:image`. |
| `CNAME` | Tells GitHub Pages to serve the site at `larasolomon.com.au`. |
| `.nojekyll` | Disables Jekyll so `index.md` is served as raw Markdown instead of being rendered. |

### Regenerating the images

Both PNGs are rendered from SVG with macOS built-ins (no image libraries required). `qlmanage`
always writes a square thumbnail, so the share card is authored on a 1200×1200 canvas with the card
content vertically centred, then cropped to the middle 630 rows:

```bash
qlmanage -t -s 1200 -o out og.svg && sips -c 630 1200 out/og.svg.png --out og-image.png
qlmanage -t -s 180 -o out favicon.svg && cp out/favicon.svg.png apple-touch-icon.png
```

## Editing

Edit the file, commit, push. GitHub Pages redeploys in about a minute.

**Keep `index.html` and `index.md` in sync** — they carry the same content in two formats, and a
crawler reading only one of them should get the same facts. Same for the summary in `llms.txt`.

When content changes, update the date in: the `dateModified` field in the JSON-LD block and the
footer `<time>` of each HTML page changed, the footer line in `index.md`, the `Last updated` line in
`llms.txt`, and `<lastmod>` in `sitemap.xml`.

### Rules for the JSON-LD entity graph

The Person node is the point of the whole site — it is what lets search engines and AI assistants
tell this Lara Solomon apart from the several others. Two rules keep it useful:

- **`sameAs` carries identity profiles only** — other pages *about this person* that she controls:
  LinkedIn, the OEIS wiki user page, GitHub. It is not a link list. The clinic's and Redrew's
  websites were removed from it deliberately; they are organisations, not identities, and they are
  correctly expressed through `worksFor` and `owns` instead. Putting them back weakens the signal.
- **Every URL in `sameAs` must resolve.** A dead identity link lowers entity confidence rather than
  raising it. In particular, if the LinkedIn vanity URL ever changes, it must be updated here, in
  `about/index.html`, in `oeis/index.html`, in `index.md` and in `llms.txt` — five places.

The Person `@id` is `https://larasolomon.com.au/#lara` on every page, so all three pages describe
one entity rather than three.

## DNS

The apex domain is registered at Crazy Domains and points at GitHub Pages:

```
A     @     185.199.108.153
A     @     185.199.109.153
A     @     185.199.110.153
A     @     185.199.111.153
CNAME www   larasolomon.github.io.
```

## Verifying the crawler setup

```bash
curl -sI https://larasolomon.com.au/ | head -1
curl -s https://larasolomon.com.au/llms.txt | head -20
curl -s https://larasolomon.com.au/robots.txt | head -10
```

Structured data can be checked with Google's
[Rich Results Test](https://search.google.com/test/rich-results) and
[Schema Markup Validator](https://validator.schema.org/).
