# All Star Embroidery

All Star Embroidery builds and maintains the software that supports our custom apparel, embroidery, headwear, bulk-order, and WooCommerce operations.

This organization is the home for our production WordPress plugins, supplier integrations, automation workflows, release tooling, and internal development systems.

## Platform architecture

```text
SanMar / S&S Activewear / Momentec
                ↓
         GitHub automation
                ↓
      Supplier integration layer
                ↓
      WordPress + WooCommerce
                ↓
 Storefront / ASBO / customer tools
```

Our repositories are organized around clear ownership boundaries:

- **Storefront & WordPress plugins** — customer-facing and administrative functionality used on the All Star Embroidery website.
- **Supplier infrastructure** — private integrations, catalog normalization, inventory updates, media processing, and supplier API/SFTP workflows.
- **Release & deployment tooling** — controlled packaging and delivery of production plugin releases.
- **Business-specific tools** — systems such as bulk ordering, product discovery, and school/varsity-jacket workflows.

## Engineering principles

- WooCommerce remains the customer-facing source of truth for products and orders.
- Supplier credentials and sensitive operational data stay private and are never committed to repositories.
- Supplier systems communicate through controlled GitHub/WordPress integration boundaries rather than exposing credentials to the storefront.
- Production automation should be understandable, reversible, and conservative with destructive changes.
- Shared product concepts such as pricing, taxonomy, sizes, inventory, and media should be normalized consistently across suppliers.
- Manual merchant changes should be preserved unless a workflow explicitly owns that data.

## Repository standards

Each production repository should clearly document:

- what the project owns;
- what it does **not** own;
- its production dependencies;
- how it is released or deployed;
- required GitHub Actions secrets by **name only**;
- how to test changes safely;
- rollback or recovery procedures where applicable.

Organization-wide engineering and migration documentation lives in the [`All-Star-Embroidery/.github`](https://github.com/All-Star-Embroidery/.github) repository.

---

**All Star Embroidery** · Newark, Ohio
