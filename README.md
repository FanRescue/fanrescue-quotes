# Fan Rescue — Installation Quotes

Hosting for individual installation and M&E design quotes for Fan Rescue Ltd.
Each quote is a single HTML file at the repo root.

**Live at:** `https://quotes.fanrescue.co.uk` (deployed via Cloudflare Pages)

---

## Quote URL pattern

```
https://quotes.fanrescue.co.uk/{filename-without-.html}
```

For example, a file named `piccadilly-grill-FR-2041.html` is served at:
`https://quotes.fanrescue.co.uk/piccadilly-grill-FR-2041`

---

## Creating a new quote

1. **Copy the template** from `/_template/installation-quote-template.html` to the repo **root**
2. **Rename** it: `{client-slug}-FR-{NNNN}.html`
   - Slug: lowercase, hyphen-separated, no spaces. e.g. `piccadilly-grill`, `joy-king-lau`
   - Reference: `FR-` followed by 4 digits — same format as cleaning proposals so they're sortable together
3. **Find & replace** all `{{DOUBLE_BRACE}}` placeholders (see template header for full list)
4. **Edit scope blocks** in Section 4 to match the job
5. **Update investment amount + payment schedule** in Section 5
6. **Delete optional sections** if not relevant:
   - The "indicative" notice bar near the top (if quote is firm)
   - The "subject to confirmatory site visit" callout (same reason)
   - The cleaning upsell section (Section 8) if not applicable
7. **Commit + push** → live within 30 seconds via Cloudflare Pages

---

## Reference numbering

Installation quotes use **`FR-XXXX`** (4 digits) — the same format as cleaning proposals.
This keeps both proposal types in a single sortable namespace and means there's no mental gear-shift between them.

Examples:
- Cleaning: `FR-2035` (Burgrill Clapton), `FR-2036` (Joy King Lau)
- Installation: `FR-2040`, `FR-2041`, etc.

Keep a running ledger of refs used (suggest: a pinned issue in this repo, or a Google Sheet) so we don't accidentally double-issue a number.

---

## Sister repos

| Subdomain | Repo | Purpose |
|---|---|---|
| `assets.fanrescue.co.uk` | `fanrescue-assets` | Logos, brand tokens (`tokens.css`), company info (`company.json`) |
| `proposals.fanrescue.co.uk` | `fanrescue-proposals` (existing) | Cleaning proposals — same template style |
| `quotes.fanrescue.co.uk` | **`fanrescue-quotes`** (this repo) | Installation & M&E design quotes |
| Portal (future) | TBD | Two-tab index of all live proposals/quotes, auto-pulled from both repos |

All three repos pull styling, logos, and company data from `assets.fanrescue.co.uk` — so a brand change is made in one place and propagates everywhere.

---

## Design system

The template uses brand tokens from `assets.fanrescue.co.uk/brand/tokens.css`:

- **Navy Deep** `#0A1628` (primary background)
- **Gold** `#C8973E` (accent)
- **Archivo Black** (display / headings / wordmark)
- **Source Sans 3** (body / UI)

Don't hardcode colours or font names in individual quote files — use CSS variables (`var(--fr-navy-deep)`, `var(--fr-gold)`, `var(--fr-font-display)`, etc).

---

## Tracking

Each quote includes a tracking pixel that pings `proposal-tracker.office-33b.workers.dev` on:
- Page load (a view)
- Accept Quote click
- Download PDF click

The `window.__frRef` value at the bottom of each quote **must match** the `QUOTE_REF` placeholder. The template fills both automatically when you do the find-and-replace.

---

## Privacy

- The repo root (`index.html`) shows a generic holding page — it does NOT index live quotes
- All quote pages have `<meta name="robots" content="noindex, nofollow">`
- `robots.txt` disallows all crawlers
- Quotes are private and only accessible via direct link

The public-facing portal (separate repo, to come) is the only place quotes are indexed.

---

## Deployment

Connected to **Cloudflare Pages**. Push to `main` → live within ~30 seconds. No build step.

### One-time setup

1. Create GitHub repo `fanrescue-quotes`
2. Push this folder's contents to `main`
3. Cloudflare → Pages → Create project → connect → leave build settings blank
4. Custom domain → `quotes.fanrescue.co.uk` (you'll need to add a CNAME at your DNS host pointing to the `*.pages.dev` URL Cloudflare provides)

---

_Maintained by Ben — Fan Rescue Ltd._
