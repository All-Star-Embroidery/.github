# All Star Embroidery

All Star Embroidery builds and maintains the software that supports our WordPress/WooCommerce storefront, supplier integrations, product operations, releases, and internal business tooling.

## What lives here

### Storefront Plugins

Customer-facing and merchant-facing WordPress/WooCommerce features such as product discovery, bulk ordering, varsity jacket experiences, navigation/header tools, and other storefront workflows.

### Supplier Infrastructure

Integrations and automation that connect approved suppliers to normalized WooCommerce product data while keeping expensive processing off the production web server whenever practical.

Current supplier infrastructure supports SanMar, S&S Activewear, and Momentec Brands.

### Releases & Deployment

Versioned plugin releases, GitHub-based update channels, deployment automation, and bounded GitHub Actions workflows used to support production systems.

### Internal Tools

Engineering utilities, migration tooling, diagnostics, documentation, and operational systems that support the storefront and supplier platform. Most internal source and operational documentation is private.

## Engineering principles

- Preserve working production behavior and improve it incrementally.
- Keep credentials and private supplier/customer data out of source control.
- Prefer GitHub-hosted automation for CPU-heavy supplier, catalog, and image work instead of loading the WordPress server.
- Keep supplier/data ownership separate from customer-facing bulk-order pricing and UX responsibilities.
- Use controlled storefront taxonomy and canonical WooCommerce product data instead of leaking raw supplier conventions into the customer experience.
- Keep GitHub Actions schedules economical and least-privileged.
- Treat repository transfers, updater changes, and production releases as controlled deployment changes.

## Organization standards

Public-safe engineering standards are maintained in this organization's `.github` repository:

- [Architecture overview](../docs/ARCHITECTURE.md)
- [Repository standards](../docs/REPOSITORY-STANDARDS.md)
- [Repository migration checklist](../docs/MIGRATION-CHECKLIST.md)
- [Contributing guidance](../CONTRIBUTING.md)
- [Security policy](../SECURITY.md)

Sensitive architecture details, supplier credentials, authenticated payloads, deployment runbooks, and production procedures are intentionally kept out of public repositories.
