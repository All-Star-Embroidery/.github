# Security Policy

All Star Embroidery repositories may support production commerce, supplier integrations, and customer-facing WordPress systems.

## Do not disclose secrets publicly

Never commit or post:

- supplier usernames, passwords, API keys, or SFTP credentials;
- WordPress bridge tokens or authentication headers;
- database credentials or backups;
- customer/order personal information;
- private API responses containing account-specific data;
- production cookies, sessions, or access tokens.

If a credential is exposed, treat it as compromised and rotate it promptly. Removing it from the latest commit is not sufficient by itself.

## Reporting a security concern

Do not open a public issue containing exploit details, credentials, or sensitive production information. Contact an All Star Embroidery organization owner through an established private business channel and provide the affected repository, impact, reproduction details, and any relevant non-secret logs.

## Secret scope

Use the narrowest practical scope:

- supplier credentials should normally remain restricted to the private supplier-integration repository/environment that actually talks to that supplier;
- shared organization secrets should be limited to selected repositories;
- public repositories must never require embedded production secrets.

## Production write safety

Workflows that modify production catalog, price, inventory, or media data should authenticate through approved secret storage, validate incoming data, and fail closed when data is incomplete or ambiguous.

## Dependencies

Security-related dependency updates should be evaluated promptly, but production updates must still preserve compatibility with the deployed WordPress/PHP/WooCommerce environment.
