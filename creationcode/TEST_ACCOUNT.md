# Test-account requirements

Create a dedicated staging identity before any Claude client test:

- synthetic human account and isolated tenant;
- approved OAuth client for Claude/Claude Code with only the six documented scopes;
- server-held binding to the sample repository and `main` base branch;
- staging GitHub App installation with minimum required repository permissions;
- separate PostgreSQL/rate-limit/approval/idempotency state;
- no production OAuth, GitHub, executor or database credentials;
- maximum build cost no greater than the locally tested Plan ceiling (currently USD 2.00 fixture; founder must ratify the real test ceiling);
- ability to revoke the OAuth grant and GitHub installation immediately;
- operator access to correlation/trace/build identity and safe audit evidence.

Exercise one client at a time first. Run a duplicate/concurrent approval test only against the disposable sample job. Preserve exact outputs, but redact tokens and grant values.
