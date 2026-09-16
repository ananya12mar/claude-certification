## Cost Orchestration — Revision Notes

- **Goal:** Keep cost, latency, and reliability within budget.

- **Core metrics (instrument every call):**
  - **Token usage:** input & output tokens
  - **Latency:** per-call ms
  - **Error rate:** per-call / per-dependency

- **Instrumentation:** wrap each API call to log tokens, latency, and errors; use traces to find slow/expensive steps.

- **Primary levers:** model selection; prompt/context size; number of tool calls; streaming vs batching; prompt caching.

- **Streaming:** accumulate deltas and only act after stream closes; retry whole request on mid-stream failures; streaming improves perceived latency.

- **Prompt caching (when to use):**
  - Cache stable, long prefixes (system prompts, tool schemas).
  - Economics: writes cost more, reads are cheap — cache only when reads >> writes.
  - TTL matters (default 5m; 1h option); exact-match prefixes required.

- **Batches API:** use for non-urgent, high-volume jobs to reduce per-request cost; check current discounts.

- **Multi-agent orchestration:**
  - Pattern: lead plans -> parallel subagents -> synthesize.
  - Use when tasks split into independent subtasks.
  - Cost impact: large multiplier (≈15x tokens reported); prefer expensive lead + cheaper subagents.
  - Reliability: multiplies failure surface; apply the same retry/backoff/fallback per subagent.

- **Reliability floor:** define latency ceilings and retry budgets first; only optimize cost above that floor.

- **Quick checklist:**
  - Instrument every call.
  - Identify the expensive/slow step before optimizing.
  - Favor caching, batching, or orchestration only when workload fits.
  - Enforce reliability via evals and gates.

Keep this file as a quick reference while building observability and orchestration features.
