## Parallel Fan-out — Revision Notes

- **Problem:** Fan-out increased cost dramatically with little quality gain.

- **Root cause:** Subagents multiplied token usage; task was not parallelizable.

- **Key fact:** Each subagent spends its own tokens and context. Multi-agent setups can multiply token cost (≈15x reported).

- **When to use fan-out:**
  - Tasks that decompose into independent subtasks (e.g., broad research across many sources).

- **When to avoid:**
  - Tightly coupled workflows where steps depend on previous outputs (e.g., iterative coding steps).

- **Actionable checklist:**
  - Run a single-agent baseline and measure tokens & quality.
  - Assess task parallelizability before adding subagents.
  - If using fan-out, use an expensive lead + cheaper subagents and apply per-agent retry/backoff.
  - Monitor per-call token usage and enforce cost/quality gates.

- **Lesson:** Orchestration is a hiring decision—only pay for parallelism when the work truly benefits.

Keep this as a quick reference when considering orchestrator-worker designs.
