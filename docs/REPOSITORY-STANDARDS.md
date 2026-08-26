# Repository Standards

These are the default engineering standards for repositories in the All Star Embroidery GitHub organization. A repository may add stricter project-specific rules, but it should not silently weaken security, release, or data-safety expectations.

## 1. Repository purpose

Each repository should have one clear primary responsibility. Prefer separation between:

- storefront/customer-facing WordPress plugins;
- supplier/data infrastructure;
- release/distribution repositories;
- internal engineering and operational tools.

Avoid combining unrelated production systems simply because they share the All Star Embroidery brand.

## 2. Naming

Preferred repository slugs are short, descriptive, and lowercase kebab-case, for example:

- `supplier-sync`
- `product-sync`
- `product-finder`
- `bulk-order`
- `varsity-jackets`
- `header-designer`

The organization name already provides the All Star Embroidery context, so new repositories should not need an `ASE.` prefix.

Product names may still be styled normally in documentation and user interfaces, such as **Supplier Sync**, **Product Finder**, **ASBO**, or **Varsity Jackets**.

Do not rename or transfer an existing production repository solely to satisfy this convention. Renames and migrations must be treated as controlled deployment changes.

## 3. Visibility

Use **private** by default for source repositories containing production implementation details, supplier integration logic, internal tooling, operational documentation, or deployment procedures.

Use **public** only when there is a deliberate reason, such as organization community-health files, public release assets, intentionally open source code, or public documentation that has been reviewed for sensitive information.

A public repository must not contain credentials, private supplier payloads, customer information, private operational runbooks, or internal-only architecture details.

## 4. Default branch and change discipline

- Use `main` as the default branch unless a legacy repository requires otherwise.
- Keep commits focused and descriptive.
- Prefer pull requests for production-impacting changes when practical.
- Repository-specific testing and release requirements take precedence over the organization defaults.
- Avoid unrelated refactors during urgent fixes.
- Preserve known working production behavior unless the change explicitly intends to alter it.

## 5. WordPress / WooCommerce projects

WordPress plugins should keep production server work bounded and predictable.

- Do not move CPU-heavy supplier normalization or image processing into WordPress when GitHub-hosted workers already handle it effectively.
- Preserve WooCommerce data ownership boundaries and merchant-owned/manual data.
- Treat product attributes, variation identity, pricing, taxonomy, and updater behavior as production data contracts.
- Version plugin releases consistently and verify the published artifact after release.
- GitHub-based plugin update mechanisms must be preserved through repository moves or release-repository changes.

## 6. Supplier infrastructure

Supplier-specific source fields should be normalized behind shared storefront concepts rather than leaking raw supplier conventions into WooCommerce.

Supplier integration code should distinguish among:

- authoritative supplier unit buy cost;
- reference-only MSRP/MAP/list values;
- supplier quantity price breaks;
- inventory;
- taxonomy and discovery facets;
- supplier-owned metadata versus merchant-owned/manual metadata.

Supplier Sync provides WooCommerce base price and supplier cost intelligence. Customer-facing bulk tier behavior belongs to ASBO/bulk-order code and must remain a separate responsibility.

## 7. Actions strategy

GitHub Actions should be reliable, least-privileged, and economical.

- Keep the default `GITHUB_TOKEN` permission set restrictive; grant write permissions only to jobs that require them.
- Declare workflow/job `permissions` explicitly for production workflows.
- Pin third-party actions to reviewed versions; for sensitive workflows, prefer immutable commit SHAs where practical.
- Use `workflow_dispatch` for safe manual execution of important workers or maintenance workflows.
- Use concurrency controls where overlapping runs could duplicate work or corrupt state.
- Keep schedules aligned to actual business freshness requirements and Eastern Time behavior where relevant.
- Do not introduce five-minute polling or other high-frequency schedules without a demonstrated need.
- Queue workers and live inventory workers should remain separate when they have different freshness and cost requirements.
- Prefer daytime scheduling for catalog/image/hydration workloads unless overnight execution has a clear purpose.

## 8. Secrets strategy

Secrets belong in approved secret storage, never source code.

Preferred order:

1. repository or environment secrets for credentials used by only one repository/environment;
2. organization secrets with access limited to selected repositories when multiple repositories truly need the same credential;
3. WordPress-stored credentials only when the application architecture genuinely requires WordPress to authenticate directly.

Additional rules:

- never commit secret values, access tokens, private keys, supplier passwords, or authenticated payloads;
- do not print secrets into Actions logs or diagnostic output;
- do not copy secrets between repositories merely for convenience;
- rotate credentials after a migration if exposure or scope is uncertain;
- document the *purpose and ownership* of a secret, not its value;
- keep production and test credentials separated when supported.

## 9. Releases and updater compatibility

A repository that publishes WordPress plugin releases should document:

- canonical plugin version source;
- release tag convention;
- release ZIP/artifact naming;
- updater repository/release endpoint expectations;
- any WordPress-side GitHub update settings that must change after migration;
- verification steps after release.

Repository migration is not complete until the WordPress updater path has been tested against the new canonical release location.

## 10. Documentation minimum

Production repositories should normally include:

- `README.md` — purpose, boundaries, setup, and operational overview;
- project-specific testing/release notes where needed;
- security guidance when the project has special handling requirements;
- a clear distinction between public-safe documentation and private operational details.

Organization-wide `CONTRIBUTING.md`, `SECURITY.md`, issue templates, and pull-request guidance are inherited from the public `.github` repository unless a repository intentionally overrides them.

## 11. Migration rule

Do not transfer, rename, archive, or replace a production repository as part of unrelated cleanup. Use `docs/MIGRATION-CHECKLIST.md` and obtain explicit approval for each repository migration.
