# All Star Embroidery · Organization Configuration

This public `.github` repository provides the organization profile and shared GitHub community-health defaults for All Star Embroidery repositories.

It is intentionally limited to **public-safe standards and guidance**. Supplier credentials, private payloads, production runbooks, detailed deployment procedures, customer data, and sensitive implementation documentation belong in private repositories.

## Organization foundation

### Public profile

- [`profile/README.md`](profile/README.md) — organization overview shown on the All Star Embroidery GitHub profile.

### Shared repository defaults

- [`CONTRIBUTING.md`](CONTRIBUTING.md) — organization-wide contribution guidance.
- [`SECURITY.md`](SECURITY.md) — default security/reporting policy.
- [`SUPPORT.md`](SUPPORT.md) — default support guidance.
- [`PULL_REQUEST_TEMPLATE.md`](PULL_REQUEST_TEMPLATE.md) — shared pull-request checklist.
- [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/) — shared bug and feature-request forms.

Repositories may provide project-specific versions of these files when they need stricter or more specialized guidance.

### Engineering standards

- [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) — high-level system architecture and responsibility boundaries.
- [`docs/REPOSITORY-STANDARDS.md`](docs/REPOSITORY-STANDARDS.md) — naming, visibility, Actions, secret, release, and repository conventions.
- [`docs/MIGRATION-CHECKLIST.md`](docs/MIGRATION-CHECKLIST.md) — controlled checklist for repository moves/renames and updater-safe migrations.

## Key boundaries

- WordPress/WooCommerce is the customer-facing commerce platform.
- GitHub hosts source control, releases, and heavier automation that should stay off the production web server when practical.
- Supplier infrastructure normalizes supplier data and supplier cost information.
- ASBO/bulk-order code owns customer-facing bulk tier calculation and bulk-order UX.
- GitHub Actions should remain least-privileged and economically scheduled.
- Production repository transfers require explicit approval and migration verification.

## Security

Never commit credentials, access tokens, supplier passwords, private customer information, authenticated supplier payloads, or production secrets to this repository or any public repository.
