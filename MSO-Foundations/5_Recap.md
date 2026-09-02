## Recap — Revision Notes (Five Takeaways)

- **1 — Tokens:**
  - Tokens are the unit of input, output, and cost.
  - Think and budget in tokens (not words); monitor usage for billing and limits.

- **2 — Context window:**
  - Fixed token budget holding full request (prompts, history, docs, outputs).
  - Oversized input = validation error; exceeding during generation = truncated output (model_context_window_exceeded).
  - App should trim or summarize history to manage long sessions.

- **3 — Sampling & non-determinism:**
  - Models sample from a token distribution → same prompt can vary across runs.
  - Avoid exact-text tests; use property/assertion tests and model-graded evals for meaning.

- **4 — Model vs reasoning:**
  - Model choice (capability) and reasoning mode (thinking depth) are separate, composable levers.
  - Start with the smallest model and minimal reasoning that pass your evals; increase only if needed.

- **5 — Technical access patterns:**
  - Access via REST API or SDKs; choose SDKs to reduce boilerplate.
  - Response modes: synchronous, streaming (SSE), async/await, or batch for bulk jobs.

- **Quick checklist:**
  - Track tokens and costs.
  - Implement history trimming/summarization.
  - Design tests that assert properties, not verbatim outputs.
  - Start with Sonnet (balanced) and minimal reasoning; eval before changing tiers.
  - Use streaming for long UX responses; use Batch API for offline bulk work.

---

Keep this card for quick revision when designing prompts, tests, and system architecture.
