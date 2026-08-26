# Repository Standards

These standards are the default for repositories owned by All Star Embroidery. A repository may document stricter project-specific rules when needed.

## Naming

Prefer short, descriptive, lowercase kebab-case names once projects live inside the organization.

Examples:

- `supplier-sync`
- `product-sync`
- `product-finder`
- `bulk-order`
- `varsity-jackets`

Avoid repeating the organization name in every repository unless it prevents real ambiguity.

## Visibility

Default to **Private** for:

- production source containing business logic;
- supplier integrations;
- infrastructure and deployment tooling;
- repositories that reveal private operational architecture unnecessarily.

Use **Public** only when the repository intentionally distributes public artifacts, open-source code, or organization-level documentation.

Public repositories must never contain credentials, private supplier data, customer information, production database exports, or authenticated API responses.

## Required README sections

Every production repository should explain:

1. **Purpose** — one paragraph describing what the project owns.
2. **Non-goals / boundaries** — what belongs in another project.
3. **Architecture** — major components and external dependencies.
4. **Development/testing** — how changes are verified.
5. **Deployment/release** — how production receives a change.
6. **Configuration** — required environment variables or secret **names**, never values.
7. **Operations** — scheduled jobs, queues, or recurring processes when relevant.
8. **Recovery/rollback** — how to return to the previous known-good state.

## Secrets

- Never commit credentials to source control.
- Store supplier credentials in the narrowest repository or environment scope that needs them.
- Organization-level secrets should be used only for genuinely shared infrastructure and restricted to selected repositories when possible.
- WordPress/storefront code should not receive supplier credentials merely for convenience.
- Documentation may list secret names and their purpose but never their values.
- Rotating a shared credential must include a documented dependency check so production workflows are not silently broken.

## GitHub Actions

Scheduled workflows should be justified by an operational need.

- Preserve `workflow_dispatch` for important operational jobs so an authorized maintainer can run them manually.
- Avoid frequent polling when there is no realistic need for near-real-time behavior.
- Queue workers should exit quickly when there is no work.
- Stagger supplier jobs when they share the same WordPress bridge or another constrained resource.
- Keep private-repository Actions usage within the organization's monthly budget.
- Store expensive image/data processing in GitHub when doing so reduces load on production WordPress safely.
- Every workflow that writes to production should validate its input before sending it.
- Inventory workflows should refuse ambiguous or partial updates instead of silently applying incomplete data.

## Production safety

Prefer changes that are:

- idempotent;
- reversible;
- ownership-aware;
- validated before write;
- conservative when supplier data is incomplete;
- explicit about migrations.

Do not delete historical products, orders, variations, or merchant-authored content during routine synchronization unless the project has a specifically approved destructive workflow.

## Releases

Production plugins should use semantic versioning and maintain a changelog.

A release should have:

- a unique version;
- reproducible or recoverable source;
- syntax/build validation;
- a clear changelog;
- an updater/release artifact that matches the tagged/source version;
- a rollback path to the prior release.

Temporary release-building workflows or files should be removed after publication when they are not part of normal operations.

## Repository descriptions and topics

Each repository should have a concise description understandable without opening the code. Use topics consistently where useful, for example:

`wordpress`, `woocommerce`, `supplier-sync`, `github-actions`, `inventory`, `all-star-embroidery`.

## Branches and pull requests

For production repositories:

- `main` represents the intended production/default line.
- Meaningful changes should be testable before merge.
- Avoid force-pushing shared production history.
- Prefer small, focused commits and PRs when multiple people are contributing.
- Automated agents must explain material production changes in the commit/PR description.

## Ownership boundaries

When unsure where a change belongs, use `docs/ARCHITECTURE.md` as the first decision point. Do not solve a downstream presentation problem by introducing supplier-specific behavior into the wrong layer unless there is a documented reason.
