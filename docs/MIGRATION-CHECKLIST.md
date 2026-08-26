# Repository Migration Checklist

Use this checklist before transferring an existing production repository into the All Star Embroidery organization.

The goal is to preserve production behavior while making the organization—not a personal account—the long-term home of the project.

## Phase 1 — Inventory before transfer

- [ ] Confirm the repository's purpose and intended new name.
- [ ] Decide whether it should be Public or Private.
- [ ] Record the current default branch.
- [ ] Review GitHub Actions workflows and identify scheduled/manual jobs.
- [ ] Record required repository/environment secret **names**.
- [ ] Identify deploy keys, webhooks, GitHub Apps, external integrations, and environments.
- [ ] Search source/workflows for hard-coded references to the current `owner/repository` path.
- [ ] Identify WordPress updater URLs, release feeds, package URLs, badges, documentation links, or API callbacks tied to the current repository path.
- [ ] Confirm whether another repository depends on releases, raw files, artifacts, or Actions from this repository.
- [ ] Confirm a known-good production release/version before migration.

## Phase 2 — Prepare organization destination

- [ ] Confirm the GitHub App/integration used for development has access to the organization.
- [ ] Confirm the intended team/member permissions.
- [ ] Confirm Actions are allowed for the repository type.
- [ ] Decide which secrets remain repository-scoped and which genuinely belong at organization/environment scope.
- [ ] Ensure supplier credentials stay restricted to the smallest appropriate scope.
- [ ] Confirm the repository name does not collide with an existing organization repository.

## Phase 3 — Transfer

- [ ] Transfer the repository to `All-Star-Embroidery`.
- [ ] Rename it only if the rename is part of the approved migration plan.
- [ ] Confirm issues, PRs, releases, branches, tags, and Actions history are present.
- [ ] Confirm repository visibility remained correct.
- [ ] Confirm the GitHub App still has access.

## Phase 4 — Repair references

GitHub redirects old repository URLs after transfer, but production should not intentionally depend on redirects long term.

- [ ] Update local Git remotes.
- [ ] Replace hard-coded old owner/repository references in source and workflows.
- [ ] Update Actions references to organization paths.
- [ ] Update release/update URLs.
- [ ] Update documentation and badges.
- [ ] Update any external integration that stores the old repository identity explicitly.
- [ ] Update cross-repository references in other All Star Embroidery projects.

## Phase 5 — Verify secrets and automation

- [ ] Confirm every required Action secret is available without exposing its value.
- [ ] Confirm organization secrets are restricted to only the repositories that need them.
- [ ] Run a safe manual workflow when the project has one.
- [ ] Verify scheduled workflow syntax after migration.
- [ ] Confirm production write workflows still authenticate successfully.
- [ ] Confirm Actions usage/billing is attributed as expected.

## Phase 6 — Production verification

For WordPress/WooCommerce projects, verify applicable items:

- [ ] Plugin updater still discovers the current release.
- [ ] A release package can be downloaded successfully.
- [ ] WordPress bridge/status checks succeed.
- [ ] Inventory workflows can fetch targets and complete without unmatched rows.
- [ ] Supplier catalog/import workflows still operate.
- [ ] Manual merchant-owned data remains untouched.
- [ ] Front-end storefront behavior is unchanged.
- [ ] No duplicate products, media, or variations were created merely because repository ownership changed.

## Phase 7 — Documentation and cleanup

- [ ] Update the repository README to the organization standard.
- [ ] Add a concise repository description and appropriate topics.
- [ ] Document scheduled workflows and their cadence.
- [ ] Document deployment/release and rollback procedures.
- [ ] Remove obsolete migration-only code or temporary workflows.
- [ ] Keep the old-path redirect available naturally through GitHub; do not create duplicate repositories at the old location.

## Recommended migration order

Start with a low-risk repository that does not control supplier inventory, production credentials, or the WordPress updater. Validate the organization setup there first.

Move production supplier automation and release infrastructure only after the lower-risk transfer has proven that GitHub App access, Actions, permissions, and release behavior work correctly in the organization.
