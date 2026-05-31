# Xotl

Landing page for [xotl.ai](https://xotl.ai/). A private research operation focused on capital allocation.

Static site, no build step. Plain HTML and CSS in a single file, one web font, inline SVG icons. It loads fast and deploys to GitHub Pages as is.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The whole site (markup, styles, structured data, cookie notice, analytics). |
| `og-image.png` | 1200x630 social preview image. Referenced by the Open Graph and Twitter tags. |
| `robots.txt` | Allows search engines and AI crawlers. Points to the sitemap. |
| `sitemap.xml` | Single-page sitemap for search engines. |
| `llms.txt` | Plain-text summary for AI and LLM tools, following the llmstxt.org convention. |
| `CNAME` | Tells GitHub Pages the custom domain is `xotl.ai`. |
| `.nojekyll` | Disables Jekyll processing so files are served exactly as committed. |

Keep every file in the repository root. The site uses absolute URLs like `https://xotl.ai/og-image.png`, so the files must sit at the domain root, not in a subfolder.

## Deploy on GitHub Pages

1. Create a public repository and push these files to the default branch (for example `main`).
2. In the repository, go to **Settings > Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**, pick `main`, folder `/ (root)`, and save.
4. Wait a minute, then the site is live at `https://<username>.github.io/<repo>/`.

That URL works immediately. The custom domain below is the next step.

## Custom domain (xotl.ai)

`xotl.ai` is an apex domain (no `www`), so it needs A records, not a CNAME at the root.

**1. Verify the domain first.** In GitHub, go to your profile (or organization) **Settings > Pages > Add a domain**. GitHub gives you a `TXT` record to add at your DNS provider. This prevents domain takeover and is worth doing before anything else.

**2. Add the DNS records** at your registrar:

Four A records for the apex (`xotl.ai`), each pointing to a GitHub Pages IP:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

Optional but recommended, four AAAA records for IPv6:

```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

One CNAME record for the `www` subdomain, pointing to your GitHub Pages domain:

```
www.xotl.ai  ->  <username>.github.io
```

**3. Set the domain in the repo.** In **Settings > Pages > Custom domain**, enter `xotl.ai` and save. This keeps the `CNAME` file in the repo in sync.

**4. Enforce HTTPS.** Once DNS resolves (this can take up to a day), tick **Enforce HTTPS**. GitHub issues a free certificate automatically.

The `CNAME` file in this repo already contains `xotl.ai`, so if you deploy from a branch you can skip editing it. Do not point the apex domain with a CNAME record; DNS does not allow CNAME at the root, and GitHub will reject it.

## After it goes live

The code is done. Getting found is the part that happens off the page. In order of value:

1. **Submit the sitemap.** Add the site to [Google Search Console](https://search.google.com/search-console) and [Bing Webmaster Tools](https://www.bing.com/webmasters), verify ownership, and submit `https://xotl.ai/sitemap.xml`. A new domain will not show up in search until it is indexed, so do this on day one.
2. **Build a few real links.** Point your X profile at the site, and add `xotl.ai` to the scholarly profiles tied to your paper (Google Scholar, ORCID, ResearchGate). Early links from places search engines already trust matter more than anything on the page.
3. **Confirm the structured data.** Run the live URL through Google's [Rich Results Test](https://search.google.com/test/rich-results) and the [Schema Markup Validator](https://validator.schema.org/) to confirm the Organization, Person, and FAQ data parse.
4. **Publish over time.** A single page is an anchor, not a body of work. Real research posted on the domain is what compounds visibility with both search engines and AI tools.

## Editing notes

- **Analytics.** [GoatCounter](https://www.goatcounter.com/) is loaded at the bottom of `index.html`. It is cookieless. The only cookie the site sets is the consent flag from the notice bar.
- **Cookie notice.** The bar uses an implied-consent model. Because GoatCounter sets no tracking cookies, the site arguably needs no banner at all. If you ever add tools that do set cookies, switch to an explicit accept and reject banner to stay clear under GDPR.
- **Social image.** If you change the wordmark or tagline, regenerate `og-image.png` at 1200x630 to match.
- **Not legal advice.** The site states plainly that Xotl is not a fund, adviser, or dealer and does not give financial advice. If the operation ever changes scope, have a securities lawyer review the wording.

## Credits

Typeface: IBM Plex Mono, served from Google Fonts (SIL Open Font License, free for commercial use).
