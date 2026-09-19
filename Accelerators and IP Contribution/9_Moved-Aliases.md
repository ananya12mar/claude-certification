**Moved Aliases — Revision Notes**

- **Problem:** Using a moving alias led to an unexpected model change in production and no rollback point.

**Failure pattern**

- Deployed alias (convenient) → upstream alias advanced → output shape changed → downstream parser failed.
- No pinned prior snapshot retained → rollback impossible; hotfix required.

**What to record**

- Always pin the model to a fixed snapshot in production.
- Keep the prior snapshot available for immediate rollback.
- Version prompts and assets alongside the model.

**Preventive checklist**

- Replace alias with pinned model ID in deployment configs.
- Retain previous snapshot and artifact metadata (checksums, version).
- Gate promotions via evals and CI (canary → baseline compare → promote/rollback).
- Add automated checks for output shape/schema changes in tests.

**Quick tips**

- Use CI to block unpinned deploys to production.
- Log deployed model ID and artifact checksum with releases.

Keep this checklist with the deployment runbook.
