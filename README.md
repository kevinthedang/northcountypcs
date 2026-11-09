# North County PCs

Marketing site for **North County PCs** — custom PC builds, upgrades, and tune-ups in
Oceanside, California and the surrounding North County area.

Built with [Astro](https://astro.build/), statically rendered. There is no client-side
JavaScript by default.

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
| `src/pages/index.astro` | The entire site: hero, services, pricing, process, service area, contact |
| `src/pages/404.astro` | Custom not-found page (built to `404.html`, which Pages serves automatically) |
| `src/layouts/BaseLayout.astro` | Shared `<head>`, header, main wrapper, and footer |
| `src/components/Header.astro` | Brand, primary nav, and call button |
| `src/components/Footer.astro` | Address, phone, and copyright |
| `src/styles/global.css` | Design tokens, layout, dark mode, responsive rules |
| `public/favicon.svg`, `public/robots.txt` | Static files copied unchanged into the build |
| `astro.config.mjs` | Site URL and sitemap integration |
| `package.json`, `package-lock.json` | Astro, build scripts, and dev dependencies |
| `.github/workflows/test.yml` | CI: type-check, build, and validate HTML on push/PR |
| `.github/workflows/audit.yml` | Dependency audit on push/PR and weekly |
| `tsconfig.json`, `.htmlvalidate.json` | Astro/TypeScript and HTML validation config |

The sitemap is generated at build time at `/sitemap-index.xml`; `robots.txt` points to it.
`_internal/` is not published — only `public/` and the built pages are deployed.

## Local preview

```sh
npm install
npm run dev
```

Then open <http://localhost:4321>.

To check the production build:

```sh
npm run build
npm run preview
```

## Tests

```sh
npm test
```

That runs three things:

1. `astro check` — Astro, TypeScript, and template diagnostics.
2. `astro build` — verifies the production build succeeds.
3. `html-validate "dist/**/*.html"` — checks the built pages for HTML and accessibility issues.

The same command runs in CI via `.github/workflows/test.yml` on pushes to `master` and
`dev`, and on pull requests.

### Dependency audit

```sh
npm run audit
```

That runs `npm audit --audit-level=high`, so the command fails on high or critical
vulnerabilities. `.github/workflows/audit.yml` runs it on pushes, pull requests, and once a
week at 8am Pacific — it schedules both 15:00 and 16:00 UTC and skips whichever isn't 8am
locally, so it stays correct across daylight saving time.

## Before launch — replace the placeholders

Every invented value is marked with a `<!-- TODO -->` comment in the source. Search for `TODO`:

```sh
grep -rn TODO src
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
- [ ] **Domain** — `northcountypcs.com` is used in `astro.config.mjs`, the canonical and
      Open Graph tags in `src/pages/index.astro`, the JSON-LD block, and
      `public/robots.txt`. Update them all if the domain differs.
- [ ] **Open Graph image** — add `og:image` (1200×630) once you have a logo or photo.

## Deploying

The site is fully static. Point the host at this repository and have it run:

```sh
npm ci
npm run build
```

Then serve `dist/`. This works on Cloudflare Pages, Netlify, Vercel, or GitHub Pages with an
Actions-based build. Set the build output directory to `dist`.

If the host needs a custom domain or `CNAME`, configure that in the host's settings.

## SEO notes

The JSON-LD block is a schema.org `ComputerStore` entry with `areaServed` for Oceanside,
Carlsbad, Vista, San Marcos, Encinitas, Escondido, Fallbrook, and Camp Pendleton. It is what
feeds Google's local results, so keep the name, address, and phone there identical to your
Google Business Profile listing — inconsistent NAP data hurts local ranking more than any
on-page tweak helps.

Shared markup lives in `src/layouts/BaseLayout.astro` and `src/components/`. Add new pages
as `.astro` files in `src/pages/`; the header, footer, and `<head>` come along automatically.
If this grows into a blog or a set of service-area pages, look at Astro content collections
so the copy and metadata stay in data files rather than hand-written markup.
