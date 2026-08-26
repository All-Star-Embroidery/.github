# Contributing to All Star Embroidery Projects

All Star Embroidery repositories support production business systems. Contributions should optimize for clarity, safety, and maintainability rather than cleverness.

## Before changing code

- Read the repository README and architecture notes.
- Confirm the change belongs in that repository's ownership boundary.
- Identify whether the change touches production data, pricing, inventory, customer orders, media, authentication, or scheduled automation.
- Never add credentials or sensitive production data to commits, issues, pull requests, logs, or test fixtures.

## Change expectations

A production change should explain:

- the problem being solved;
- the intended behavior after the change;
- what was deliberately left unchanged;
- how the change was tested;
- any migration or one-time repair behavior;
- rollback considerations when applicable.

Prefer idempotent migrations and ownership-aware updates. Manual merchant changes should not be overwritten unless the project explicitly owns that field and the behavior is documented.

## Testing

Use the narrowest meaningful test first. For supplier/catalog systems, validate normalized data before writing to WordPress. For inventory, reject ambiguous or incomplete source coverage. For WordPress plugins, perform syntax/build checks and verify the affected admin/front-end workflow.

Never use production customer orders as disposable test data.

## Pull requests

When pull requests are used, keep them focused. Include screenshots for meaningful visual changes and concise evidence for behavior changes. Call out changes to schedules, secrets, permissions, external APIs, pricing, or production writes prominently.

## Releases

Do not publish a production plugin release unless version metadata, changelog, package contents, updater metadata, and recoverable source agree on the same version.
