# Security Policy

All Star Embroidery repositories support storefront, supplier-integration, release, and internal business systems. Security-sensitive information must be handled privately and with least privilege.

## Reporting a security issue

Do **not** publish credentials, access tokens, supplier secrets, private customer information, authenticated supplier payloads, exploit details, or other sensitive material in public issues, pull requests, discussions, Actions logs, screenshots, or test fixtures.

If you believe you have found a security issue affecting an All Star Embroidery project, contact an organization owner through an established private business channel. Include the affected repository/project and enough non-sensitive detail to begin investigation safely.

A repository may provide a more specific `SECURITY.md`; repository-specific reporting instructions take precedence when present.

## Secret handling

- Never commit secret values to source control.
- Prefer repository/environment secrets for credentials used by one repository or environment.
- Use organization secrets only when multiple repositories genuinely require the same credential, and restrict access to selected repositories.
- Prefer GitHub-hosted secret storage over WordPress-stored supplier credentials when the system architecture permits.
- Keep production and test credentials separated when supported.
- Do not expose secrets in Actions logs or diagnostic output.
- Rotate credentials when exposure or migration scope is uncertain.

Documentation may describe a secret's purpose and owner, but never its value.

## GitHub Actions security

Production workflows should follow least privilege:

- keep default `GITHUB_TOKEN` permissions restrictive;
- declare the minimum workflow/job `permissions` required;
- grant write permissions only where the workflow actually needs them;
- review third-party actions and pin sensitive dependencies to immutable versions/commit SHAs where practical;
- avoid running untrusted pull-request code with production secrets;
- keep manual production workflows bounded and clearly named;
- prevent accidental overlapping runs where duplicate work could damage data or waste Actions minutes.

## Public repository boundaries

Public repositories must not contain:

- production credentials or tokens;
- private supplier/customer data;
- authenticated supplier payloads;
- private operational runbooks;
- sensitive deployment procedures;
- internal-only architecture or access-control details.

Public documentation should remain high-level and safe to disclose. Detailed production procedures belong in private repositories.

## Production data safety

Automation must fail safely when supplier or external data is incomplete, contradictory, or ambiguous. Supplier-owned normalized data must not silently overwrite merchant-owned/manual data outside the documented ownership boundary.

Security fixes should preserve working production behavior where possible and include a bounded verification and rollback plan.
