# Support and incident path

## Non-sensitive support

Open a GitHub issue at <https://github.com/marino129/creationloop-mcp/issues> with:

- connector/client surface and version;
- UTC timestamp;
- CreationCode correlation and trace IDs;
- tool name and result/error class;
- whether the issue reproduced in the isolated test account.

Do not paste OAuth tokens, approval URLs/grants, GitHub credentials, repository secrets, full conversation content, exact private Requests, or customer data.

## Security or privacy incident

1. Disable/disconnect CreationCode in Claude.
2. Revoke the CreationCode OAuth connection through the selected provider.
3. Stop further submission/build/merge calls; do not retry an ambiguous mutation.
4. Preserve only safe IDs, timestamps, build SHA and result class.
5. Open a **private** GitHub security advisory: <https://github.com/marino129/creationloop-mcp/security/advisories/new>.

The founder must supply a monitored direct support/privacy contact and response targets before directory publication. Until then, this package remains blocked.
