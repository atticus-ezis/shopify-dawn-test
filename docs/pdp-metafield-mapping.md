# Product page metafield mapping

Source of truth: [`.shopify/metafields.json`](../.shopify/metafields.json) (aligned with the assignment metafield documentation).

| Metafield | Type | Where it appears | Fallback when blank |
|-----------|------|------------------|---------------------|
| `global.description` | Multi-line text / HTML | Middle column — `global_description` block in [`sections/main-product.liquid`](../sections/main-product.liquid). Renders option links and the gray `.metafield-description-table` spec card. | Block outputs nothing (no empty wrapper). |
| `custom.about` | Rich text | Middle column — `about` block. Heading from Theme Editor; body via `metafield_tag`. | Block outputs nothing. |
| `custom.sas_compatible` | Boolean | Buy box — [`snippets/product-buy-box.liquid`](../snippets/product-buy-box.liquid). Required acknowledgement checkbox before add to cart. Label from section setting `sas_checkbox_label`. | Checkbox hidden. |
| `custom.zoned_storage` | Boolean | Buy box — same pattern as SAS. Label from section setting `zoned_checkbox_label`. | Checkbox hidden. |
| `custom.product_short_name` | Single-line text | `product-details` section **heading** in [`templates/product.json`](../templates/product.json) (`heading` setting bound to the metafield). | Heading blank → visually-hidden accessibility title only. |
| `custom.warranty` | Rich text | `product-details` — Warranty accordion when **Use product warranty metafield** is enabled. | Accordion row hidden when blank. |
| `custom.packaging` | Rich text | `product-details` — Packaging accordion when **Use product packaging metafield** is enabled. | Accordion row hidden when blank. |
| `custom.series` | Single-line text | Specification accordion table — [`snippets/product-specifications-table.liquid`](../snippets/product-specifications-table.liquid). | Row omitted. |
| `custom.model_number` | Single-line text | Specification accordion table. | Row omitted. |
| `custom.part_number` | Single-line text | Specification accordion table. | Row omitted. |
| `custom.form_factor` | Single-line text | Specification accordion table. | Row omitted. |
| `custom.capacity` | Single-line text | Specification accordion table. | Row omitted. |
| `custom.interface` | Single-line text | Specification accordion table. | Row omitted. |
| `custom.spindle_speed` | Single-line text | Specification accordion table. | Row omitted. |
| `custom.tray` | Single-line text | Specification accordion table. | Row omitted. |
| `custom.width` | Single-line text | Specification accordion table. | Row omitted. |
| `custom.height` | Single-line text | Specification accordion table. | Row omitted. |
| `custom.depth` | Single-line text | Specification accordion table. | Row omitted. |

## Specification table (hybrid sources)

Rendered in `product-details` when the row has **Use product specification metafields** enabled:

| Label | Source |
|-------|--------|
| Type | `product.type` |
| Brand | `product.vendor` |
| Series | `custom.series` |
| Model Number | `custom.model_number` |
| Part Number | `custom.part_number` |
| Form Factor | `custom.form_factor` |
| Capacity | `custom.capacity` |
| Interface | `custom.interface` |
| Spindle Speed | `custom.spindle_speed` |
| Tray | `custom.tray` |
| Weight | Variant `weight` + `weight_unit` |
| Width | `custom.width` |
| Height | `custom.height` |
| Depth | `custom.depth` |

Blank / zero values are omitted. If every row is blank, the Specification accordion is hidden.

## Section / snippet structure

Product-page **`product-details`** is the collapsible accordion section (Specification / Warranty / Packaging / Disclaimer), not the separate Dawn `shopify.disclosure` section.

```
templates/product.json
├── sections/breadcrumbs → snippets/breadcrumbs
├── sections/main-product
│   ├── product media gallery (Dawn)
│   ├── info column blocks (title, vendor, sku, variant_picker, global_description, about, …)
│   └── snippets/product-buy-box
│       ├── price / inventory / quantity (from diverted blocks)
│       ├── compatibility checkboxes (metafields)
│       ├── snippets/buy-buttons (product form)
│       └── trust_callout blocks (repeatable)
├── sections/divider
├── product-details → sections/collapsible-content
│   └── Specs / Warranty / Packaging / Disclaimer
│       └── snippets/product-specifications-table (Specification row)
└── sections/related-products
```

Price, inventory, quantity, buy buttons, and trust callouts are Theme Editor blocks that render in the buy box (3rd column), not the middle column.

## Differences: Figma vs live SPD vs this theme

| Area | Figma | Live Server Part Deals | This theme |
|------|-------|------------------------|------------|
| Layout | 3-column: gallery / info / buy box | Similar commercial PDP | Matches Figma structure (gallery + info + buy box) |
| Visual polish | Primary visual reference | Production styling / marketing extras | Closely matches Figma; not pixel-perfect |
| Add to cart / qty / variants | Implied | Working product form + cart | Dawn product form, quantity `name="quantity"`, cart drawer preserved |
| Currency | Shown in design | Markets / localization | Shopify Markets localization form when multiple countries available |
| SAS / zoned gating | Compatibility UX | Required checkboxes | `custom.sas_compatible` / `custom.zoned_storage` checkboxes |
| Specs / warranty / packaging | Details area | Product info panels | `product-details` accordion + metafields |
| Trust callouts | Selling-point area | Marketing promises | Theme Editor `trust_callout` blocks (heading, text, optional link) |
| Ship countdown | — | Present on live | Intentionally not ported |
| Title banner | — | Present on live | Intentionally not ported |
| Testing-protocol block | — | Present on live | Intentionally not ported |
| Related products | May appear in design | Recommendations / related | Shopify related-product recommendations section |
| Sticky mobile CTA | Mobile purchase affordance | Live mobile UX | `enable_sticky_mobile_cta` section setting |

## Assumptions and limitations

- Visual reference is the Figma 3-column buy-box layout; live Server Part Deals page is the functional reference for ATC, quantity, currency, and SAS gating.
- Live-only extras (ship countdown, title banner, testing-protocol marketing block) are intentionally not ported.
- Price per TB is derived from product tags/title capacity (`…TB`), not a metafield.
- Currency selector uses Shopify Markets / localization form when multiple countries are available.
- Related products use Shopify’s related recommendations API (no custom product-source picker or section CTA button — Dawn limitation).
- No product `condition` metafield exists in store definitions; condition is not shown as a dedicated field.
- Theme Editor screenshots/video for submission: see [`docs/submission-checklist.md`](submission-checklist.md).
