# Submission checklist (PDP developer test §8–10)

## Preview links

With `shopify theme dev --environment development` running:

| Link | URL |
|------|-----|
| Local preview | http://127.0.0.1:9292 |
| Shareable theme preview | https://server-part-deals-wbvv73ej.myshopify.com/?preview_theme_id=153391890520 |
| Sample PDP (local) | http://127.0.0.1:9292/products/seagate-exos-x18-st18000nm004j-18tb-7-2k-rpm-sas-512e-12gb-s-3-5in-refurbished-hdd |
| Sample PDP (shareable) | https://server-part-deals-wbvv73ej.myshopify.com/products/seagate-exos-x18-st18000nm004j-18tb-7-2k-rpm-sas-512e-12gb-s-3-5in-refurbished-hdd?preview_theme_id=153391890520 |
| Theme Editor | Online Store → Themes → Customize on the development theme (`153391890520`), or press `e` in the CLI session |
| GitHub repository | https://github.com/cdcdianne/server-tech-solutions-test |

Preview theme ID refreshes when you restart `shopify theme dev`; update this table if the CLI prints a new ID.

## Screenshots / video

Assets live under [`docs/submission/`](submission/).

### Completed product page

- [x] Desktop: [`docs/submission/pdp-desktop.png`](submission/pdp-desktop.png)
- [x] Mobile (390px): [`docs/submission/pdp-mobile.png`](submission/pdp-mobile.png)

### Theme Editor configurability (§8)

Theme Editor requires an authenticated Shopify Admin session — capture these manually (screen recording or stills):

- [ ] Change section visibility, spacing, background/color scheme, or alignment
- [ ] Edit product-page labels, accordion titles, section headings, supporting text
- [ ] Add, remove, or reorder trust/callout blocks
- [ ] Change related products settings (heading, product count, columns)
- [ ] Metafields populating the correct UI (about, global description, specs, warranty, packaging, SAS/zoned)
- [ ] Graceful fallback when a metafield is empty (hide accordion row / block / checkbox)
- [ ] Desktop and mobile previews in the Theme Editor

Save Theme Editor captures as `docs/submission/theme-editor-*.png` or `docs/submission/theme-editor-demo.mp4`.

## Supporting notes (already in repo)

| Artifact | Path |
|----------|------|
| Metafield mapping | [`docs/pdp-metafield-mapping.md`](pdp-metafield-mapping.md) |
| Structure + assumptions | Same doc — “Section / snippet structure”, “Assumptions and limitations” |
| Figma vs live vs implementation | Same doc — “Differences: Figma vs live SPD vs this theme” |

## Quick smoke test before submit

- [ ] PDP loads with no Liquid errors
- [ ] Add to cart with selected quantity
- [ ] Variant change updates price / availability / ATC state
- [ ] Empty metafields leave no blank table rows or empty accordions
- [ ] No horizontal scroll on mobile
- [ ] Sticky mobile CTA does not cover content or fight the cart drawer
