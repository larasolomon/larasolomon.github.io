# larasolomon.com.au

Personal website for Lara Solomon, served as a static site from GitHub Pages at
<https://larasolomon.com.au/>.

## Files

| File | Purpose |
|---|---|
| `index.html` | The site. Single page, no JavaScript, inline CSS, light/dark aware. Includes schema.org JSON-LD. |
| `index.md` | Plain-Markdown mirror of the page content, for text-only readers and LLM crawlers. |
| `llms.txt` | Structured summary for language models ([llmstxt.org](https://llmstxt.org/) convention). |
| `robots.txt` | Explicitly allows every search and AI crawler by name. |
| `sitemap.xml` | Sitemap covering the page, the Markdown mirror and `llms.txt`. |
| `CNAME` | Tells GitHub Pages to serve the site at `larasolomon.com.au`. |
| `.nojekyll` | Disables Jekyll so `index.md` is served as raw Markdown instead of being rendered. |

## Editing

Edit the file, commit, push. GitHub Pages redeploys in about a minute.

**Keep `index.html` and `index.md` in sync** — they carry the same content in two formats, and a
crawler reading only one of them should get the same facts. Same for the summary in `llms.txt`.

When content changes, update the date in three places: the `dateModified` field in the JSON-LD block
and the footer `<time>` in `index.html`, the footer line in `index.md`, the `Last updated` line in
`llms.txt`, and `<lastmod>` in `sitemap.xml`.

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
