# All Star Embroidery · Organization Configuration

This special `.github` repository contains shared GitHub configuration and documentation for the All Star Embroidery organization.

## What lives here

- `profile/README.md` — public organization profile.
- `docs/ARCHITECTURE.md` — high-level ownership boundaries between storefront, supplier infrastructure, and release systems.
- `docs/REPOSITORY-STANDARDS.md` — naming, visibility, documentation, Actions, and secret-management conventions.
- `docs/MIGRATION-CHECKLIST.md` — checklist for moving an existing repository into the organization safely.
- `CONTRIBUTING.md` — organization-wide contribution expectations.
- `SECURITY.md` — security and secret-handling expectations.
- `PULL_REQUEST_TEMPLATE.md` — default pull-request checklist.
- `.github/ISSUE_TEMPLATE/` — default issue forms for repositories that do not provide their own.

## Scope

This repository should contain **documentation and safe defaults only**. Do not commit production credentials, supplier secrets, bridge tokens, customer data, private API responses, or sensitive infrastructure details here.

Repository-specific documentation takes precedence when a project needs stricter or more specialized rules.
