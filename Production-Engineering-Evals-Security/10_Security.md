## Security — Revision Notes

- **Goal:** Defend agents from untrusted input and pass regulated reviews.

- **Primary threat:** Prompt injection — fetched content can contain hidden instructions.
  - Treat anything the agent did not author as data, never as actionable instructions.

- **Related threat:** Jailbreaks — user prompts crafted to bypass safety. Defense shape is the same: validate input + constrain actions.

- **Enforced controls (not just prompts):**
  - Hooks (pre-tool checks) that allow/deny actions and emit audit logs.
  - Least-privilege identities and scoped secrets (env or secret manager).
  - OS-level sandboxing: filesystem & network isolation.

- **Practical rules:**
  - Wrap untrusted content as data; do not let it alter permissions.
  - Keep secrets out of code; rotate via secret manager.
  - Protect auth configuration (changing roles is a privileged operation).
  - Use expensive lead + cheaper subagents if orchestration is needed (cost consideration).

- **Regulated scoping checklist:** confirm and document:
  - **Data residency:** where data is processed and whether it leaves customer boundary.
  - **Access logging:** per-action audit logs with identity and result.
  - **Managed configuration:** admin-controlled, centrally managed auth & rules.
  - **Model ZDR eligibility:** verify per-model/platform at scoping time.

- **Hook behavior example (conceptual):**
  - PreToolUse hook: block writes outside allowed paths, log blocked/allowed actions.

- **Defense mapping (quick):**
  - Prompt injection → treat as data + pre-tool hooks → log source/action/block
  - Jailbreak → input validation + action constraints → log prompt/refusal
  - Over-broad access → least privilege + locked config → log privileged actions
  - Sandbox escape → OS sandboxing → log denied access attempts

- **Tradeoffs:** layered controls add complexity and setup work but prevent single-point failures.

Keep this file as a quick security checklist while implementing hooks, scoped auth, and sandboxing.
