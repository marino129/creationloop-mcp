# CreationCode connector launch checklist

Every item is required. Nothing in this file has been executed against production.

## Evidence and code

- [x] Receipt gate `PASS` — three verified production Receipts (first `rcpt_d4b8f6e292ebb7d96f48`). Residual: production still lacks an in-band build SHA (tracked follow-up).
- [ ] Historic merge-doctrine conflict is resolved by the founder.
- [x] Receipts landed on `main` (`2e204da7`, `afb70eb1`, `eae81a31` = current main at reconciliation); stale collision manifest discarded, adapter rebuilt from current main.
- [ ] Native web and MCP call one live application-service implementation.
- [ ] Exact event/projection parity passes against a disposable database.
- [ ] Approval and idempotency migrations pass apply/concurrency/rollback in staging.
- [ ] Full unit, integration, concurrency, security, secret, typecheck, build, lint and diff checks pass.

## Configuration and operations

- [ ] Trusted OAuth provider/client registrations selected and reviewed.
- [ ] Public endpoint, protected-resource metadata, redirect URIs, Hosts and Origins reviewed.
- [ ] Distributed rate-limit, approval, idempotency and audit stores configured.
- [ ] Health endpoint proves reviewed build SHA.
- [ ] Privacy retention/deletion terms, subprocessors, region and monitored contacts approved.
- [ ] Support/privacy/security contacts and response targets monitored.
- [ ] Rollback, disable switch and incident drill exercised.

## Client proof

- [ ] Official independent MCP client passes against staging.
- [ ] Claude Code discovery, OAuth, tools, text fallback and full lifecycle pass.
- [ ] Claude web/desktop custom connector, OAuth, five views and full lifecycle pass.
- [ ] One MCP-driven production Receipt proves exact Request → verified Receipt with one run through the MCP surface.
- [ ] Real screenshots/footage replace every local fixture image.

## Founder approvals

- [ ] Draft implementation PR reviewed and explicitly approved to merge.
- [ ] Staging migration/deploy explicitly approved.
- [ ] Production migration/deploy explicitly approved.
- [ ] Connector manifest/directory copy reviewed.
- [ ] Publication/submission explicitly approved.
