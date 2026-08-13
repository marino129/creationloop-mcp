# CreationCode connector launch checklist

Every item is required. Nothing in this file has been executed against production.

## Evidence and code

- [ ] Receipt #1 Gate 0 is strict `PASS`, including retrievable Receipt and production build SHA.
- [ ] Historic merge-doctrine conflict is resolved by the founder.
- [ ] Receipt #1 landed on `main`; collision manifest rebuilt in a fresh worktree.
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
- [ ] Receipt #2 proves exact Request → verified Receipt with one run.
- [ ] Real screenshots/footage replace every local fixture image.

## Founder approvals

- [ ] Draft implementation PR reviewed and explicitly approved to merge.
- [ ] Staging migration/deploy explicitly approved.
- [ ] Production migration/deploy explicitly approved.
- [ ] Connector manifest/directory copy reviewed.
- [ ] Publication/submission explicitly approved.
