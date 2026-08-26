# All Star Embroidery Development Architecture

This document defines the intended high-level ownership boundaries for All Star Embroidery software. It is deliberately architectural rather than implementation-specific so individual projects can evolve without blurring responsibilities.

## System flow

```text
Supplier systems
(SanMar / S&S Activewear / Momentec)
        │
        ▼
Private supplier automation
(GitHub Actions, API/SFTP clients, normalization, validation)
        │
        ▼
WordPress supplier integration
(catalog cache, product linking, imports, repair, bridge endpoints)
        │
        ▼
WooCommerce
(products, variations, prices, stock, media, categories, attributes)
        │
        ├──────────────► Storefront / product discovery
        │
        └──────────────► Bulk-order experience / ASBO
```

## Responsibility boundaries

### Supplier automation

Owns:

- authentication to supplier systems;
- scheduled catalog and inventory retrieval;
- supplier-specific parsing and normalization;
- validation before data reaches WordPress;
- computationally expensive processing that should stay off the web server where practical;
- secure use of supplier credentials through GitHub Actions secrets.

Does **not** own:

- customer-facing cart calculations;
- WordPress presentation/layout;
- merchant-authored WooCommerce content.

### Supplier Sync / WordPress integration

Owns:

- receiving normalized supplier data;
- supplier identity and multi-supplier linking;
- product/variation import and repair;
- WooCommerce inventory updates;
- normalized product attributes, taxonomy, media ownership, shipping data, and supplier-backed pricing inputs;
- preserving merchant-owned changes unless Supplier Sync explicitly owns the field;
- the authenticated bridge between GitHub and WordPress.

Does **not** own:

- supplier credentials that can be kept in GitHub;
- ASBO's customer-facing cart quantity calculations;
- unrelated storefront layout.

### WooCommerce

Acts as the customer-facing product and order system of record.

Supplier systems may inform WooCommerce fields, but customers should not depend directly on supplier APIs at page-load or checkout time.

### ASBO / bulk ordering

Owns:

- customer-facing bulk-order workflow;
- quantity-tier application at cart/order time;
- embroidery/decoration options and bulk-order UX;
- interpreting the authoritative WooCommerce base price and approved bulk-pricing rules.

Supplier Sync may provide cost and price-break information, but ASBO should not independently guess supplier costs or redefine Supplier Sync's normalization rules.

### Storefront/product discovery

Owns:

- customer-facing filtering, search, product finding, and presentation;
- consuming standardized WooCommerce categories, attributes, and discovery tags.

It should rely on normalized catalog data rather than supplier-specific category names or codes.

## Planned repository roles

The organization should move toward small repositories with obvious ownership. Recommended names are illustrative until migration is approved:

| Repository role | Recommended name | Default visibility |
| --- | --- | --- |
| WordPress supplier plugin | `supplier-sync` | Private |
| Supplier/API/Actions backend | `product-sync` | Private |
| Public updater/release artifacts, if still required | `supplier-sync-releases` | Public |
| Bulk-order plugin | `bulk-order` | Private |
| Product finder | `product-finder` | Public or Private by deployment need |
| Varsity jacket tooling | `varsity-jackets` | Public or Private by deployment need |
| Header/navigation plugin | `header-designer` | Private |

Do not combine repositories merely to reduce the repository count. Merge projects only when they share a release lifecycle, security boundary, and clear ownership model.

## Data ownership rule

When more than one system can write the same WooCommerce field, the responsible project must document an ownership rule. Typical states are:

- **supplier-managed** — automatically updated from normalized supplier data;
- **merchant-managed** — manual business-owner edits are preserved;
- **derived** — calculated from another authoritative value;
- **reference-only** — stored for diagnostics or decision support but never used as the authoritative customer value.

This convention is especially important for price, inventory, media, categories/tags, shipping data, and supplier identity.
