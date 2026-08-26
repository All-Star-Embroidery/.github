# Contributing to All Star Embroidery Projects

All Star Embroidery repositories support business software, supplier infrastructure, storefront plugins, releases, and internal tooling. Contributions should prioritize production safety, clarity, maintainability, focused scope, and low operational overhead.

## Before changing code

- Read the repository-specific README and testing/release guidance.
- Confirm the change belongs in that repository's documented responsibility boundary.
- Inspect existing production behavior before replacing or refactoring working systems.
- Keep Supplier Sync responsibilities separate from ASBO/bulk-order responsibilities.
- Identify any release, updater, migration, Actions, secret, or WooCommerce data-contract impact before implementation.

Repository-specific contribution rules take precedence over this shared guidance.

## Change discipline

- Prefer incremental changes over broad rewrites.
- Avoid unrelated cleanup in production fixes.
- Preserve merchant-owned/manual data unless the change explicitly and safely owns that data.
- Keep CPU-heavy supplier normalization, image processing, and similar backend work off the WordPress server when GitHub-hosted automation is the established architecture.
- Do not introduce unnecessary high-frequency GitHub Actions schedules.
- Treat product variation identity, pricing, taxonomy, media, inventory, release artifacts, and updater behavior as production contracts.

## Pull requests

Pull requests should explain:

- the problem being solved;
- intended behavior;
- ownership/scope boundaries;
- verification performed;
- production impact;
- migration or repair behavior;
- release/update implications;
- rollback considerations when relevant.

Use the organization pull-request template unless the repository provides a more specific one.

## Security and private data

Never include credentials, customer information, private supplier data, access tokens, authenticated payloads, production secrets, or sensitive runbook content in commits, issues, pull requests, Actions logs, screenshots, or test fixtures.

Use approved GitHub secret storage and least-privileged Actions permissions. See `SECURITY.md` and `docs/REPOSITORY-STANDARDS.md` for organization defaults.

## Repository moves and renames

Do not transfer, rename, archive, or replace a production repository as incidental cleanup. Repository migrations require explicit approval and must follow `docs/MIGRATION-CHECKLIST.md`.
