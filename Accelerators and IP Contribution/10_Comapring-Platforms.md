**Comparing Platforms — Revision Notes**

- **Goal:** Evaluate latency, compliance, and total cost so procurement/security can approve platform choice.

**Latency: measure from the customer**

- Measure round-trip using the customer's region and real payload (your laptop measurements lie).
- In-region cloud typically wins latency; first-party API wins earliest access to features.
- For Bedrock, test regional vs global endpoints (residency vs cost trade-off).

**Compliance: often decisive**

- Check certifications, audit controls, and data residency per platform and per model.
- A customer's existing certified cloud usually wins (no re-certification).
- Confirm per-model hosting details for third-party vendors (e.g., Microsoft Foundry).

**Cost: beyond token price**

- Compare total cost per call including egress, platform fees, and integration effort.
- Instrument real workload cost on each candidate platform.

**Decision checklist**

- Latency test results from customer region + payload.
- Compliance matrix: certifications, residency, auditability.
- Total cost estimate: tokens, egress, fees, integration.
- Risk notes: feature parity, vendor timelines, retirement policy.

**Quick tips**

- Run small benchmarks early in scoping to avoid surprises.
- Document the measurement methods and results for procurement/security.
- If compliance is pass/fail, let that constraint drive the choice.

Keep these notes with the platform decision record.
