**Packaging a working build — Revision Notes**

- **Goal:** Turn a working build into a configurable asset that future teams configure, not rewrite.

**Asset types & packaging**

- **Agent template:** package system prompt, tool schemas, loop; parameterize domain values with documented defaults.
- **MCP server:** document each tool input and scope; make credentials and scopes configurable by reference.
- **Eval suite:** include dataset + rubric; pin baseline scores and run CI checks before promoting models.

**Core checklist (keep with the build)**

- README + quickstart (one-command install, example config).
- Parameterize customer-specific values (prompts, paths, scopes, creds by ref).
- Include CI/evals that verify behavior and guardrails (pinned baseline).
- Contribution guide and PR checklist for maintainers.
- Audit bundle: data touched, identity, and logs.
- Versioning: pin model/prompt versions and maintain a changelog.

**What to document (assumptions)**

- Environment expectations and required inputs.
- Failure modes handled and recovery steps.
- Deployment options and compliance notes (residency, IAM scope).

**Decisions to record**

- Runtime choice and rationale (latency/cost/compliance).
- Data residency and identity boundaries.
- Upgrade/rollback policy and test gates.

**Quick tips**

- Prefer a single configurable template over many one-off scripts.
- Keep tests deterministic and automatable.
- Make maintainer acceptance trivial: small diffs, clear tests, clear docs.
- For true one-offs, skip heavy packaging and note why.

**Audit reminder:** include an exportable audit log with the package for security reviews.

Keep this checklist close while you package.
