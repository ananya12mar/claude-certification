## Enterprise Integration — Revision Card

- Enterprise integration adds identity, auditability, and data-location requirements to a working prototype.
- The question is no longer “does it connect?” but “who is it acting as, what can it access, and how is it governed?”

- Authentication patterns:
  - User identity service: OAuth.
  - Service identity service: API key or managed secret.
  - Local service: filesystem permissions and deny rules.

- Secret handling:
  - Never store secrets inline in committed config.
  - Keep them in environment variables or managed secret stores.
  - Scope to the least privilege needed.
  - Rotate immediately on compromise.

- Enterprise controls:
  - managed settings lock config at org level
  - PostToolUse hooks provide audit logging
  - data residency and region choice matter for compliance

- High-risk workflow pattern:
  - explore → plan → code
  - use Plan mode before execution
  - define blast radius and approval points before work starts
  - use hooks for enforcement and audit trails

- Rule of thumb:
  - prototyping is about connectivity
  - production is about governance, identity, and auditability

Quick checklist

- Choose auth by service identity model
- Store secrets outside repo files
- Rotate compromised keys immediately
- Use managed settings for enterprise locking
- Add audit hooks for sensitive tool use
- Validate data residency / region requirements

### Q&A (flashcards)

1. **What changes in enterprise integration?**  
   Identity, auditability, secret handling, and data residency become required.

2. **When use OAuth?**  
   For user-identity based remote services.

3. **When use an API key?**  
   For service-identity remote integrations with managed secret storage.

4. **Where should secrets live?**  
   In env vars or secret managers, not committed config files.

5. **What is the purpose of managed settings?**  
   To lock org-wide configuration and prevent local override.

6. **Why add audit hooks?**  
   To record tool use for compliance and review.

7. **What is the key modernization pattern?**  
   Explore/plan/code with scoped approvals and guardrails.

8. **One-line rule?**  
   A production integration must be auditable, secret-safe, and centrally governable; a prototype is not enough.
