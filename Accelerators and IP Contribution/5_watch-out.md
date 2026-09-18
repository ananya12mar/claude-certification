**Watch Out — Revision Notes**

- **Problem:** PRs stall when a reviewer cannot verify the change quickly.

**Failure pattern**

- Author submits working code without a runnable example, test, or assumptions note.
- Reviewer must reconstruct intent and deprioritizes the PR.

**Signs a PR will stall**

- No minimal runnable example.
- No automated test showing the behavior.
- No short assumptions/requirements note.

**Pre-submit checklist**

- Add a minimal example or demo script (one-liner to run).
- Include tests (unit/integration or a small eval) that prove behavior.
- Add a short assumptions section (env, inputs, limits).
- Keep the PR focused and small; split large changes.

**Quick tips**

- Small, self-contained PRs review faster.
- Embed sample inputs/outputs in the example.
- Point reviewers to a one-line run command in the PR description.

Keep this checklist with the PR to avoid review delays.
