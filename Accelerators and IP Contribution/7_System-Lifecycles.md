**System Lifecycles — Revision Notes**

- **Goal:** Treat a Claude application as an engineered system with clear phases, artifacts, and gates.

**Lifecycle phases (map model work)**

- Requirements: capture functional behaviors and infra constraints.
- Design: pick platform, model, and trust/data boundaries.
- Build: implement agent, tools, prompts, and config.
- Test: run evals, unit, integration, and end-to-end checks.
- Deploy: pin versions; gate promotion on passing evals.
- Operate: monitor cost, latency, errors; enforce guardrails.
- Iterate: feed production findings back to requirements.

**Gates & discipline**

- A gate is a formal decision to move phases (e.g., residency satisfied before build, eval pass before production).
- Do not skip gates—especially for regulated deployments.

**Checklist (apply lifecycle)**

- Define artifacts for each phase (requirements doc, design notes, tests, pinned release).
- Define gates and acceptance criteria (SLOs, eval thresholds, residency checks).
- Automate tests and promotion gates in CI.

**Quick tips**

- Keep artifacts small and reviewable to speed approvals.
- For prototypes, collapse phases but add gates before production.

Treat the lifecycle as the enforcement model for reviewable, repeatable deployments.
