## Recap — Revision Notes

- **Set the standard first:** write evals before implementation; pick exact-match, code checks, or human judges as appropriate.

- **Trace failures precisely:** use unit/functional/integration/E2E tests and per-step traces to locate root causes.

- **Handle failures explicitly:** classify retriable vs terminal; apply exponential backoff with caps and retry budgets; provide named fallbacks.

- **Measure cost per call:** instrument tokens, latency, error rate; use fan-out only for independently parallel subtasks (multi-agent ≈15x tokens reported).

- **Treat fetched content as data:** enforce action boundaries with hooks, scope identities with least privilege, and keep secrets out of source.

- **Quick checklist:**
  - Eval first → implement second
  - Instrument & trace every call
  - Retry budget + explicit fallbacks
  - Cache, batch, or fan-out only when justified
  - Hooks + sandboxing for security & audit

- **Next module (brief):** package builds as templates/MCP servers/eval suites; choose and pin deployment surfaces (API, Bedrock, Vertex); document residency and model ZDR eligibility.

- **References:** Anthropic platform docs, Claude Code hooks, multi-agent research, and Skilljar courses (platform.claude.com, code.claude.com, anthropic.com).

Keep this as a one-page checklist while finishing productionization and packaging.
