# New Quote — Quick Start

A one-page checklist for creating a new installation quote.

---

## 1. Copy & rename

```
_template/installation-quote-template.html   →   {client-slug}-FR-{NNNN}.html
```

Place at **repo root**, not inside any folder.

**Filename rules:**
- `client-slug`: lowercase, hyphens, no spaces — `joy-king-lau`, `battersea-bloom`
- `FR-NNNN`: 4-digit number, sequential with cleaning quotes (check current ledger)

---

## 2. Find & replace placeholders

Open the file in any text editor and search for `{{` — replace every match:

| Placeholder | Example |
|---|---|
| `{{CLIENT_NAME}}` | Piccadilly Grill |
| `{{CLIENT_COMPANY}}` | Piccadilly Grill Ltd |
| `{{CONTACT_NAME}}` | Sarah Chen |
| `{{CONTACT_EMAIL}}` | sarah@piccadillygrill.co.uk |
| `{{SITE_ADDRESS}}` | 12 Piccadilly, London W1J 0DQ |
| `{{QUOTE_REF}}` | FR-2041 |
| `{{QUOTE_DATE}}` | 15 May 2026 |
| `{{INSTALLATION_TYPE}}` | Kitchen Extraction & Ventilation — Indicative Quote |
| `{{QUOTE_SHORT_DESCRIPTION}}` | One-line description for the hero subtitle |
| `{{TOTAL_EX_VAT}}` | £55,000 |
| `{{TOTAL_INC_VAT}}` | £66,000 inc. VAT |
| `{{DEPOSIT_AMOUNT}}` | £33,000 |
| `{{MIDPOINT_AMOUNT}}` | £16,500 |
| `{{COMPLETION_AMOUNT}}` | £5,500 |

⚠️ The tracking script at the bottom uses `window.__frRef = "{{QUOTE_REF}}"` — confirm find & replace caught that line too.

---

## 3. Customise scope & investment

### Section 4 — Proposed Scope of Works
- Replace `[CATEGORY NAME]` headings with real categories (e.g. "Air Handling & Ventilation")
- Replace each `[Item title]` / `[Description]` with real items
- Add or remove `<li>` items and `<div class="fr-scope-block">` blocks as needed
- Update the **Exclusions** box at the bottom

### Section 5 — Investment
- Replace the 3 `[REPLACE: ...]` bullets in `.fr-investment__includes` with the headline equipment items

---

## 4. Optional sections to delete

If the quote is **firm** (not indicative), delete two blocks:
- The gold "indicative" notice bar between hero and intro
- The "Subject to confirmatory site visit" callout at the end of Section 5

If the **cleaning upsell** isn't relevant (e.g. not a kitchen system), delete Section 8 entirely.

---

## 5. Commit & push

```bash
git add piccadilly-grill-FR-2041.html
git commit -m "Add quote FR-2041 — Piccadilly Grill"
git push
```

Or via GitHub Desktop / GitHub web UI — same effect.

Live at:
`https://quotes.fanrescue.co.uk/piccadilly-grill-FR-2041`

within ~30 seconds.

---

## 6. Send the link

Email the client a direct link. Don't expose the URL anywhere indexable — there's no portal authentication on individual quotes; security relies on the URL being private.

---

## Troubleshooting

**Logo missing in topbar / styling looks plain?**
→ Check internet connection — the template pulls from `assets.fanrescue.co.uk`. If assets are down, the page degrades to system fonts and no logo, but is still readable.

**Accept button doesn't open email client?**
→ Some browsers (Chrome on locked-down work laptops) block `mailto:` links. The fallback is the contact details in the footer.

**Tracking pixel not firing?**
→ Confirm `window.__frRef` value matches `QUOTE_REF`. If client has an ad blocker, tracking will silently fail — that's fine, doesn't affect anything visible.
