## Fetched Page — Revision Notes

- **Scenario:** Agent fetches web pages and can write to a single file path. Internal users assumed fetched pages were trusted.

- **Failure mode:** A fetched page contained an injected instruction telling the agent to write to an unexpected path; the agent treated fetched text as commands and complied.

- **Root cause:** Trusting the user does not protect against hostile content retrieved from external sources — fetched content must be treated as untrusted data.

- **Fix (two-sided):**
  - Treat fetched content strictly as data (don't let it alter prompt or permissions).
  - Add a `PreToolUse` hook to block writes triggered by untrusted input and log the attempt.

- **Checklist:**
  - Wrap fetched content as data and validate before acting.
  - Enforce action boundaries via hooks before tool execution.
  - Audit blocked attempts and allowed privileged actions.

Keep this as a quick reminder when designing web-fetching agents.
