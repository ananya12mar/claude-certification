**Trust Boundaries — Revision Notes**

- **Goal:** Identify every seam where data, identity, or secrets cross and enforce least-privilege controls so the multi-component app passes review.

**Map components before connecting**

- Draw a simple integration map listing each component, what it contributes, the seam where data crosses, and the enforcing control.

**Trust boundary principles**

- A trust boundary is where data/instructions move between environments — treat inbound content as untrusted data, not executable instructions.
- Scope each component to least privilege; the app is only as safe as its most privileged seam.

**Regulated scoping essentials**

- Record audit logging, data residency, and permission controls per component.
- Confirm platform and per-model residency/certification (e.g., ZDR, HIPAA/BAA) before finalizing design.

**Checklist (runbook items)**

- Integration map: components, seams, controls.
- Auth model: identities per component and least-privilege roles.
- Secrets: creds-by-ref, rotation policy, and vault usage.
- Input handling: validate/sanitize fetched content and enforce data-only semantics.
- Logging: audit trails for boundary crossings and access events.
- Tests: boundary-isolation tests and end-to-end checks with untrusted payloads.

**Quick tips**

- Automate secrets-by-reference and avoid embedded credentials.
- Add CI checks that simulate untrusted inputs crossing seams.
- If a seam cannot be secured, escalate and block deployment.

Keep this checklist with the integration map and runbook.
