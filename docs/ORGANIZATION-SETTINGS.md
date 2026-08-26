# Recommended Organization Settings

This document records the intended baseline for the All Star Embroidery GitHub organization. Some settings must be applied in the GitHub organization UI by an organization owner.

## Member and repository permissions

Recommended baseline:

- Require two-factor authentication for organization members.
- Keep base member permissions conservative; grant repository access intentionally.
- Restrict repository deletion and transfer to organization owners.
- Disable private-repository forking unless a real development need appears.
- Prefer team-based access as additional collaborators are added.

## Repository creation

- Default new production repositories to **Private**.
- Use Public only for intentional release/distribution repositories or public documentation.
- Prefer lowercase kebab-case project names without an unnecessary `ASE-` prefix once the repository already lives inside the organization.

## GitHub Actions

- Keep Actions enabled for approved repositories.
- Use restrictive default `GITHUB_TOKEN` permissions; grant write permissions only in workflows that require them.
- Preserve manual `workflow_dispatch` for operational supplier/deployment workflows.
- Review scheduled workflows against the monthly Actions-minute budget.
- Avoid high-frequency polling overnight when the business does not need near-real-time processing.
- Keep supplier/inventory jobs staggered when they share the WordPress bridge.

## Secrets and environments

- Use organization secrets only for values genuinely shared across more than one repository.
- Restrict organization secrets to selected repositories where possible.
- Keep SanMar, S&S, Momentec, and other supplier credentials scoped to the private supplier-integration repository/environment that requires them.
- Never place supplier credentials in public release repositories or customer-facing WordPress source.
- Use environments for production deployment credentials when approval/protection rules provide real value.

## Branch and merge policy

For production repositories after migration:

- Protect `main` when collaborative development begins.
- Require pull requests and at least one review when more than one developer is actively contributing.
- Require important CI/status checks before merge once those checks exist and are reliable.
- Prevent force pushes to protected production branches.
- Prefer squash merges for small feature/fix branches unless preserving individual commits has operational value.

Do not enable branch rules merely for appearance; rules should match the actual development workflow and should not make emergency production recovery harder without a documented bypass process.

## Security

- Enable dependency/security alerts where supported and useful.
- Enable secret scanning/push protection where available for the repository/plan.
- Review installed GitHub Apps periodically and remove access that is no longer needed.
- Keep the ChatGPT/OpenAI GitHub integration limited to repositories where development access is intended.

## Migration policy

Do not bulk-transfer all personal repositories at once. Move one lower-risk repository first, validate Actions/App access/release behavior, then migrate production supplier and updater infrastructure according to `MIGRATION-CHECKLIST.md`.
