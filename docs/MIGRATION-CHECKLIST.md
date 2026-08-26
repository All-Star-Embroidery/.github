# Repository Migration Checklist

Use this checklist before moving, renaming, or replacing any All Star Embroidery production repository.

**Hard rule:** no production repository is transferred to the All Star Embroidery organization without explicit approval for that specific repository.

A migration is a deployment change, not cosmetic cleanup. Preserve working production behavior and the existing release/update path until the replacement path is verified.

## Phase 1 — Inventory the existing repository

- [ ] Confirm the current canonical owner/repository name.
- [ ] Record the default branch.
- [ ] Identify active release tags and current production version.
- [ ] Identify GitHub Actions workflows and their schedules.
- [ ] Identify repository, environment, and organization secret dependencies by purpose only; never copy secret values into documentation.
- [ ] Identify release artifacts consumed by WordPress or other production systems.
- [ ] Identify hard-coded repository URLs, raw-content URLs, API endpoints, badges, documentation links, webhooks, or updater settings.
- [ ] Identify branch protection/rulesets and required checks.
- [ ] Identify external integrations that are authorized specifically for the current repository.
- [ ] Identify any supplier/API allowlists or credentials whose scope may depend on repository or environment.
- [ ] Confirm which system owns each production responsibility so the migration does not accidentally merge Supplier Sync and ASBO behavior.

## Phase 2 — Inspect production dependencies

For WordPress/WooCommerce plugins:

- [ ] Confirm the plugin slug and update-check mechanism.
- [ ] Confirm where WordPress expects GitHub releases to exist.
- [ ] Confirm the release ZIP filename and folder structure expected by the updater.
- [ ] Confirm any WordPress admin setting that stores a GitHub release repository or update endpoint.
- [ ] Confirm the currently installed production version.
- [ ] Confirm rollback/install-from-ZIP remains possible.

For GitHub-hosted supplier infrastructure:

- [ ] Confirm queue workers, inventory workers, catalog jobs, and image workers separately.
- [ ] Preserve economically tuned schedules unless a schedule change is intentional.
- [ ] Confirm heavy normalization/image work remains off the WordPress server.
- [ ] Confirm secret scopes and Actions permissions can be reproduced with least privilege.
- [ ] Confirm manual workflow execution remains available where it is currently part of operations.

## Phase 3 — Prepare the destination

Do not perform this phase until the migration is explicitly approved.

- [ ] Choose the final organization repository slug.
- [ ] Set the correct visibility.
- [ ] Configure repository access and GitHub App access.
- [ ] Recreate required repository/environment secrets using approved secret storage.
- [ ] Prefer organization secrets only when multiple repositories genuinely require the same credential, and scope them to selected repositories.
- [ ] Recreate required Actions settings, permissions, environments, and rulesets.
- [ ] Confirm `GITHUB_TOKEN` permissions remain restrictive by default.
- [ ] Confirm third-party actions and reusable workflows are still permitted by organization policy.
- [ ] Update documentation without exposing secret values or private supplier data.

## Phase 4 — Move or rename

- [ ] Perform the approved GitHub transfer/rename.
- [ ] Confirm the repository exists at the intended organization path.
- [ ] Confirm branches, tags, releases, issues, pull requests, and release assets are present.
- [ ] Confirm Actions workflows are enabled and reference valid secrets.
- [ ] Confirm repository permissions for maintainers and connected GitHub Apps.
- [ ] Review every workflow before manually triggering production work.

## Phase 5 — Update production references

- [ ] Update WordPress GitHub release/update settings when applicable.
- [ ] Update updater code only if required; preserve the existing update contract whenever possible.
- [ ] Update workflow cross-repository references.
- [ ] Update documentation, badges, raw-content links, and API URLs.
- [ ] Update deployment scripts or release jobs that refer to the old owner/repository.
- [ ] Update external integrations that do not follow GitHub redirects automatically.
- [ ] Do not remove the old reference path from operational notes until verification is complete.

## Phase 6 — Verification

- [ ] Read the destination repository through the normal maintainer connection.
- [ ] Perform a real, bounded write test.
- [ ] Run only the minimum safe Actions tests needed to prove permissions/secrets.
- [ ] Verify a manual workflow where manual execution is part of normal operations.
- [ ] Verify the next plugin release can be published at the new location if the repository owns releases.
- [ ] Verify WordPress can detect and install/update from the canonical GitHub release location.
- [ ] Verify supplier inventory/catalog/media behavior has not changed unless intended.
- [ ] Verify ASBO pricing/cart-tier behavior remains unchanged when the migration concerns Supplier Sync.
- [ ] Check Actions consumption after migration for accidental schedule duplication.

## Phase 7 — Rollback readiness

Before declaring the migration complete:

- [ ] Know how to reinstall the last known-good WordPress plugin ZIP if needed.
- [ ] Keep the last known-good release/tag identifiable.
- [ ] Preserve enough documentation to restore old update references if the new path fails.
- [ ] Do not delete or archive useful source/history as part of the initial migration.

## Phase 8 — Closeout

- [ ] Confirm production updater/release behavior has been verified, not merely assumed.
- [ ] Confirm no credentials were added to source during the move.
- [ ] Confirm no duplicate scheduled workflows are running from both old and new locations.
- [ ] Confirm documentation identifies the new canonical repository.
- [ ] Record the migration date and any follow-up cleanup in private engineering documentation.

Only after these checks pass should the new organization repository be treated as the canonical production location.
