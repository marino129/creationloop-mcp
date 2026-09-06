# Sample repository requirements

The launch sample must be a dedicated, non-production GitHub repository:

- installed through the approved CreationCode GitHub App/installation;
- bound server-side to one test tenant and base branch (`main` recommended);
- contains no production secrets, customer data, deploy keys, credentials or protected production workflow;
- has deterministic install, typecheck, test, lint and build commands documented in-repo;
- has branch protection/checks that CreationCode can read;
- allows CreationCode to create a feature branch and PR without giving Claude a credential;
- uses a change small enough for the bounded run and approved cost ceiling;
- includes accessibility/test acceptance criteria for visible UI changes;
- can be reset/recreated without deleting production data.

The expected proof chain must retain exact Request, exact Plan, approval subject, one run ID, candidate SHA, PR, merge approval, independent verification, public record when required and Receipt.
