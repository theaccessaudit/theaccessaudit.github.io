# Northwind Ceramics — the deliberately broken demo store

This is the subject of our published sample report. It is a FIXTURE, not a real
shop and not a real business's site.

**Why it exists.** The sample used to audit `dequeuniversity.com/demo/mars`.
That was defensible — you cannot publish an audit of a real business's failures
as marketing, so the subject has to be a site that wants to be found broken —
but Deque is a competitor, so the most prominent name in our flagship
deliverable was a rival vendor, and a mock spaceflight booking site does not
look like the boutique owner reading it.

**Why it is safe.** "Northwind" is the long-standing fictional-company name from
Microsoft's sample databases, so it reads as a fixture to anyone technical and
as a plausible shop to everyone else. Every page carries a demo banner in the
markup and `<meta name="robots" content="noindex">`. It is excluded from
`sitemap.xml`. Nothing is for sale and no payment path exists.

**The defects are deliberate. Do not "fix" them.** Each is a failure class that
actually shows up in small-shop e-commerce, which is the whole point — the
sample has to mirror the reader's own site.

| Where | Defect | Caught by |
|---|---|---|
| all pages | `*:focus { outline: none }` with nothing replacing it | keyboard walk, WCAG 2.4.7 |
| header | icon-only search and cart `<button>`, no accessible name | axe `button-name` |
| footer | icon-only social links | axe `link-name` |
| storefront | one product image with no `alt` attribute | axe `image-alt` |
| storefront | one product image with `alt="IMG_4821.jpg"` | a human — axe passes it |
| storefront | SALE badge, light orange on white | axe `color-contrast` |
| storefront | newsletter input with a placeholder and no label | axe `label` |
| product | size swatches built from `<div>` with a click handler | keyboard walk, WCAG 2.1.1 |
| product | Add to cart is a `<div>`, not a `<button>` | keyboard walk, axe |
| product | quantity `<select>` with no accessible name | axe `select-name` |
| product | both product pages share one `<title>` and description | machine readability |
| product | no `Product` structured data anywhere | machine readability |
| cart | `<html>` with no `lang` | axe `html-has-lang` |
| cart | icon-only Remove controls | axe `button-name` |

**Regenerating the sample after editing anything here:**

```bash
cd ~/a11y-venture/scanner
bun scan.ts https://theaccessaudit.github.io/demo-store/ --pages 8
cp ../reports/theaccessaudit.github.io-<date>.html ../site/sample-report.html
```

The crawl scope stops at `/demo-store/`, so it cannot wander into the real site.
