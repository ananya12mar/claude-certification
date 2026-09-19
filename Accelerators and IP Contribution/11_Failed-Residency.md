**Failed Residency — Revision Notes**

- **Problem:** Team chose familiar platform; it failed the customer's residency/compliance review and required a costly rebuild.

**Failure pattern**

- Team defaults to familiar cloud for speed → build passes functional tests → security review discovers residency mismatch → placement rejected.

**Signs to watch**

- Customer is regulated or mentions residency/certifications during scoping.
- Platform lacks documented regional hosting or audit controls for the required region.

**Pre-scoping checklist**

- Ask: required data residency, certifications, and audit responsibilities.
- Map acceptable platforms for those constraints before design.
- Record the chosen platform's hosting form and evidence it meets residency.

**Mitigation steps**

- Prefer early scoping conversations over late rewrites.
- If forced to prototype on a familiar platform, label it clearly and schedule porting before production.

**Quick tips**

- Put residency as a gating question in the requirements doc.
- Confirm per-model hosting details for third-party vendors (e.g., Microsoft Foundry).

Keep this checklist with the project scoping notes.
