# OAuth scopes and permissions

| Scope                          | Permits                                                            | Does not permit                                              |
| ------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------ |
| `creationcode:chat`            | Start a non-authoritative thread, retain messages, prepare a draft | Submit a Request, spend, build, merge, or issue a Receipt    |
| `creationcode:jobs:read`       | Read server-bound Job, Plan, run and PR projections                | Start/retry a run or write GitHub                            |
| `creationcode:requests:submit` | Submit exact retained Request bytes with direct approval           | Change repository or approve a Plan                          |
| `creationcode:builds:approve`  | Approve exact Plan/cost/budget and reserve its sole run            | Raise cost, start a second run, or access GitHub credentials |
| `creationcode:merges:approve`  | Authorize at most one merge attempt for exact PR/SHA/checks        | Infer success, bypass reread, or create a Receipt            |
| `creationcode:receipts:read`   | Retrieve an already-derived verified Receipt                       | Create, alter, or infer one                                  |

The connector resolves human, tenant, client, repository, base branch, and GitHub installation on the server. These values are not accepted from tool arguments. Consequential tools additionally consume a short-lived, single-use approval grant bound to the exact object and current state.

Users should deny unexpected scopes, disable irrelevant tools, and disconnect the connector to revoke access. Team/Enterprise owners should keep high-risk mutation tools disabled until staging proof and policy review are complete.
