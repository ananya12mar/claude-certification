Moving an asset from private reuse into shared infrastructure a maintainer accepts
You have already done most of the work that makes an asset shareable. When you packaged it for your own team to reuse, you pulled out the parameters, wrote down the assumptions, and bundled the eval. The parameters show the asset can be configured rather than rewritten. The documented assumptions tell the maintainer what environment the asset expects. The bundled eval gives them a way to confirm it still works. An asset packaged for internal reuse is already close to what a maintainer needs to accept it.

**Contributing Back — Revision Notes**

- **Goal:** Move a packaged asset from private reuse into a channel maintainers accept.

**Match the channel**

- Choose the right destination (Cookbook for focused examples, repo for tools/servers, project repo for full apps).
- Mismatch (e.g., full app → Cookbook) stalls review.

**Maintainer verification checklist**

1. Single responsibility: the contribution does one clear thing.
2. Runnable example: reviewer can run behavior without building a harness.
3. Test: automated proof that the feature works.
4. Assumptions: short statement of environment, inputs, and limits.

**Legal & attribution gate**

- Confirm contribution rights (customer IP, third-party code). Add attribution and license info before technical review.

**Contribution readiness checklist**

- README: purpose, quickstart, and config examples.
- Example: minimal runnable demo with sample config.
- Tests: CI-friendly unit/integration checks and evals.
- License/CLA: confirm rights and add attribution notes.
- PR notes: reviewer checklist, upgrade impact, and changelog entry.

**Quick tips**

- Keep PRs small and focused for faster reviews.
- Provide a simple script to run the example (one-liner).
- Use creds-by-reference and avoid shipping secrets.
- If licensing blocks contribution, escalate to the owner — don't push it.

Keep this checklist with the asset when opening a contribution.
