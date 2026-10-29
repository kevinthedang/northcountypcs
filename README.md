# North County PCs

Marketing site for **North County PCs** — custom PC builds, upgrades, and tune-ups in
Oceanside, California and the surrounding North County area.

Static HTML and CSS. No build step, no dependencies, no JavaScript.

## Scope

Offered, and safe to promise today:

- Custom PC builds (specced, assembled, cable-managed, stress-tested)
- Upgrades — SSD, RAM, GPU, PSU, cooling
- Tune-ups and fresh Windows installs, including data migration to a new drive
- Free first look, and an honest opinion on upgrade vs. replace

Deliberately **not** offered. The site says these are referred out:

- Board-level repair
- Data recovery from a failed drive (one wrong spin can destroy the only copy)
- Virus and malware removal — not comfortable promising it yet

Keep the page honest: if a service line gets added back, it should appear in the services
list, in the `<title>`/description if it matters for search, and in the JSON-LD description.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The entire site: hero, services, pricing, process, service area, contact |
| `style.css` | Design tokens, layout, dark mode, responsive rules |
| `404.html` | Custom not-found page (GitHub Pages serves this automatically) |
| `favicon.svg` | Browser tab icon |
| `robots.txt`, `sitemap.xml` | Search engine discovery |

## Local preview

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Before launch — replace the placeholders

Every invented value is marked with a `<!-- TODO -->` comment in the HTML. Search for `TODO`:

```sh
grep -n TODO index.html
```

- [ ] **Phone number** — `(760) 555-0100` / `tel:+17605550100` appears in the header,
      hero, contact panel, footer, and the JSON-LD block.
- [ ] **Email address** — `hello@northcountypcs.com`, same five places.
- [x] **Diagnostic credit** — the $49 full diagnostic is **credited toward the repair** if the
      quote is accepted (not refunded; declining still costs $49). Quoted on the site and in the
      JSON-LD offer description.
- [ ] **Credit threshold** — decide whether the credit applies to every repair or only above a
      set amount. On a job cheaper than $49 the credit eats the whole ticket.
- [x] **Self-taught disclosure** — the repair-first band states plainly that the business is
      self-taught and will refer out work that's outside its ability. Keep that true: the line is
      only worth having if a no-thanks referral actually happens.
- [ ] **Repair-first promise** — the site publicly says you'd rather save a machine than sell
      a new one, and that you won't invent reasons to upsell. If a build would genuinely serve
      the customer better, quote the build rather than quietly steering them to a repair.
- [ ] **Once you're comfortable with virus removal**, add it back to the service list — it's
      high-demand and high-margin. Don't promise it before then.
- [ ] **Diagnostic fee amount** — $49 is still a placeholder. Confirm it (and the `price` and
      `priceRange` values in JSON-LD).
- [ ] **What "free" covers** — the checklist promises a check of power, boot, and obvious
      faults with no obligation. Make sure you're happy honoring that on the bench, including
      for machines you turn away.
- [ ] **Diagnostic scope** — the home page promises outcomes (confirmed fault, hardware tested,
      written findings, data untouched), not a step-by-step method. The actual procedure lives
      in `_internal/diagnostic-sop.md`. Keep the promises on the page true to what you do.
- [ ] **Drop-off address** — currently "address provided when you book". Add a street
      address here and to the `PostalAddress` in JSON-LD once you have one.
- [ ] **Hours** — currently "By appointment, Monday–Saturday".
- [ ] **Domain** — `northcountypcs.com` is used in the canonical tag, Open Graph tag,
      `sitemap.xml`, and JSON-LD. Update all five if the domain differs.
- [ ] **Open Graph image** — add `og:image` (1200×630) once you have a logo or photo.

## Deploying

GitHub Pages, from `master`:

1. Repository → Settings → Pages.
2. Source: *Deploy from a branch*, branch `master`, folder `/ (root)`.
3. If you use a custom domain, add a `CNAME` file containing the bare domain and enable
   **Enforce HTTPS**.

## SEO notes

The JSON-LD block is a schema.org `ComputerStore` entry with `areaServed` for Oceanside,
Carlsbad, Vista, San Marcos, Encinitas, Escondido, Fallbrook, and Camp Pendleton. It is what
feeds Google's local results, so keep the name, address, and phone there identical to your
Google Business Profile listing — inconsistent NAP data hurts local ranking more than any
on-page tweak helps.

If the site grows past a few pages, the hand-written nav and footer will need to be
duplicated in every file. At that point move to a static site generator (Astro or Eleventy)
rather than maintaining the copies by hand.
