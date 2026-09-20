**Seam Boundary — Revision Notes**

- **Problem:** Components pass isolated tests but the unmarked seam allows untrusted content to be executed downstream.

**Failure pattern**

- Component A fetches external content → passes its tests → forwards content directly into Component B's prompt/inputs → Component B executes unintended instructions.

**Key principle**

- Every data crossing between deployment environments is a trust boundary. Treat inbound content as untrusted data and enforce controls at the seam.

**Seam checklist**

- Identify every seam in the integration map.
- Add boundary controls: input validation, schema checks, and explicit data-only semantics.
- Sanitize or redact fields that could be interpreted as instructions.
- Enforce least privilege and scoped credentials at the seam.
- Add tests that simulate malicious or malformed fetched content.

**Quick tips**

- Never pass fetched content directly as executable prompts.
- Log seam crossings and add alerts for schema violations.

Keep this checklist with the integration map and runbook.
