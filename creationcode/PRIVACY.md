# Privacy and data retention (pre-publication draft)

## Data CreationCode must retain to provide proof

- authenticated account/tenant/client identifiers and server repository binding;
- CreationChat messages supplied for the job;
- the exact visible Final Request bytes and SHA-256;
- exact Plan, Plan hash, maximum cost, execution budget and human approval evidence;
- run reservation, bounded execution events, costs and artifact/candidate hashes;
- pull-request number, candidate SHA, checks, merge intent/attempt and independent verification;
- Trust Ledger/public record evidence where current product behavior requires it;
- Receipt and its retrievable identifiers;
- correlation/trace IDs, result class, rate-limit and idempotency outcomes.

## Secrets that must not be placed in MCP data or logs

OAuth bearer tokens, approval-grant values, GitHub installation credentials, executor credentials, and unnecessary conversation/request content are excluded from telemetry. GitHub credentials remain server-side and are never sent to Claude Code.

## Retention and deletion

CreationCode's exact proof objects are intentionally durable, but the production retention duration, account deletion/export procedure, subprocessors, data-region statement, and privacy contact are not yet ratified in the supplied evidence. Publication is blocked until the founder supplies and approves those terms. Directory copy must not claim a retention duration before that decision.

Test accounts must use synthetic data and an isolated repository. Never put customer secrets, production data, access tokens, or private keys in CreationChat, a Request, or a test repository.
