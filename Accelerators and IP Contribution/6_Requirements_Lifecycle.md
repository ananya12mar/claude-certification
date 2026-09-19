**Requirements Lifecycle — Revision Notes**

- **Goal:** Convert a business problem into checkable functional and infrastructure requirements that justify deployment choices.

**Functional requirements**

- Write behavior as testable statements (e.g., "classify ticket into 4 queues", "draft reply; never auto-send").
- Each functional item should map to an eval or acceptance test.

**Infrastructure requirements (derive early)**

- Latency: response target measured at user location.
- Scale: expected QPS and peak load.
- Residency: data location and applicable regulations.
- Identity & audit: who acts, credentials, and required logs.

**Documenting & defending decisions**

- Keep a short requirements record: functional items, infra constraints, and source (business/regulation).
- Use this record to justify runtime, region, and compliance choices during reviews.

**Checklist (capture before platform choice)**

- Functional: list of checkable behaviors + associated evals.
- Latency: SLO and measurement point.
- Scale: expected throughput and peak.
- Residency: required regions and legal notes.
- Identity: auth model and audit logging requirements.

**Quick tips**

- Elicit infra constraints early—it's cheaper than retrofitting.
- For prototypes with no review, capture lightweight notes and revisit before production.

Keep this checklist with the project requirements.
