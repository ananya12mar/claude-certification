**Deployment & Versioning — Revision Notes**

- **Goal:** Choose the deployment platform to meet identity/residency needs and pin model/prompt versions to avoid silent production changes.

**Platform choice (match customer cloud)**

- Platform decisions are typically driven by the customer's cloud, identity, and compliance posture.
- Confirm hosting form for third-party vendors (e.g., Microsoft Foundry) and residency implications at build time.

**Versioning rules**

- Pin model IDs to fixed snapshots (avoid unpinned aliases) and version prompts and assets alongside code.
- Retain prior snapshots for rollback. Verify platform-specific pinning conventions at build time.

**Promotion & gating**

- Gate promotions with evals: canary traffic → compare vs baseline → promote or roll back.
- Use CI to enforce eval checks before full rollout.

**Deployment strategies & artifacts**

- Canary, blue/green, phased rollouts; region-aware routing for residency.
- Produce immutable artifacts (containers, bundles) with checksums and store in a registry.

**Checklist (release readiness)**

- Pin model/prompt versions in repo and config.
- Add eval gate and CI checks tied to promotion.
- Define rollout strategy, SLOs, and rollback criteria.
- Build immutable artifact and publish with checksum.
- Log deployment: version, artifact checksum, region, and approver.

**Quick tips**

- Small, frequent releases with clear changelog ease rollbacks.
- Use feature flags for behavior changes; keep cred-by-ref for secrets.
- Verify platform-specific model pinning policy at build time.

Record all decisions in the release notes to keep audits and rollbacks traceable.
