# Organization Architecture

This document describes the public, high-level architecture and ownership boundaries for All Star Embroidery software. Sensitive implementation details, credentials, supplier payloads, deployment internals, and production procedures belong in private repositories.

## System model

All Star Embroidery development generally follows this flow:

**WordPress / WooCommerce ↔ GitHub-hosted services and automation ↔ Approved suppliers and external services**

WordPress and WooCommerce remain the customer-facing commerce platform. GitHub hosts source control, releases, automation, normalization workers, and other workloads that are better kept off the production web server. Supplier integrations provide catalog, pricing, inventory, media, and product metadata according to each supplier's supported interfaces.

## Major responsibility areas

### Storefront plugins

WordPress plugins own customer-facing and merchant-facing behavior inside the storefront. Examples include product discovery, bulk ordering, navigation/header tools, varsity jacket experiences, and other site features.

Storefront plugins should remain focused on presentation, WooCommerce integration, configuration, and bounded application logic. Expensive supplier processing or image normalization should be moved to GitHub-hosted workers when practical.

### Supplier infrastructure

Supplier Sync and related backend automation normalize supplier data into stable WooCommerce concepts. Current supplier integrations include SanMar, S&S Activewear, and Momentec Brands.

Supplier infrastructure is responsible for supplier-specific API/feed handling, exact valid variation matching, inventory synchronization, authoritative unit buy cost, normalized media, controlled product taxonomy, and safe import/update behavior.

Supplier infrastructure must not independently own customer-facing bulk tier calculations. Those belong to the bulk-order application.

### Bulk ordering / ASBO

ASBO owns customer-facing bulk-order pricing and order-flow behavior. Supplier Sync provides correct WooCommerce base pricing and supplier cost intelligence, but it does not replace ASBO's cart-tier calculations.

Changes that alter bulk tier logic, bulk checkout behavior, or ASBO-specific customer UX should be handled in the ASBO project rather than folded into Supplier Sync.

### Releases and deployment

GitHub is the source of truth for versioned source and release artifacts. WordPress plugins that support GitHub-based updates must preserve their existing updater/release contract when maintained or migrated.

Production release changes should be incremental, testable, reversible where practical, and verified after publication.

### Internal tools

Operational utilities, migration helpers, diagnostics, import tooling, and engineering documentation should be kept separate from storefront code when they are not required at runtime. Private operational details belong in private repositories.

## Data and security boundaries

- Credentials and access tokens must never be committed to source control.
- GitHub Actions secrets or other approved secret stores should be preferred over WordPress-stored supplier credentials when architecture permits.
- Supplier-owned normalized data must not silently overwrite merchant-owned/manual data outside its documented ownership boundary.
- Public repositories must not contain private supplier payloads, customer data, production credentials, or sensitive operational runbooks.
- Automated updates should fail safely when source data is incomplete or ambiguous.

## Resource strategy

The production WordPress server should stay lightweight. CPU-heavy supplier normalization, image processing, hydration, and queue work should be performed through GitHub-hosted automation where practical.

GitHub Actions schedules should be economical and aligned to actual freshness requirements. High-frequency polling should not be introduced unless there is a demonstrated operational need.

## Repository organization

Repositories should be organized by clear product or infrastructure responsibility rather than by a generic `ASE.` prefix. Names should remain short, descriptive, and understandable within the All Star Embroidery organization context.

See `docs/REPOSITORY-STANDARDS.md` for repository conventions and `docs/MIGRATION-CHECKLIST.md` for the controlled migration process.
