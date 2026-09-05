## Extended Thinking — Revision Notes

- **What it is:** model generates a reasoning (thinking) block before the final answer; reasoning is adaptive and tuned via `effort` (not `budget_tokens`).

- **Cost:** thinking tokens bill like output tokens — enable only when extra reasoning adds value.

- **When to enable:**
  - Multi-step reasoning (math derivations, multi-hop logic, dependent planning).
  - Agentic planning across tool calls (budget planning step rather than per call).
  - Not for mechanical lookups, extraction, or simple classification.

- **Carry-back rule (crucial):**
  - Any thinking block returned by the API must be sent back unchanged on the next turn (signature-verified).
  - Do not edit, summarize, or drop thinking blocks; doing so will cause API rejection.

- **Redacted thinking:** encrypted/hidden reasoning is also immutable — return it unchanged.

- **Practical checklist:**
  - Start with reasoning off; enable when evals show multi-step failure.
  - Tune `effort` to the problem depth; avoid high effort for simple tasks.
  - Preserve thinking blocks verbatim in tool-use loops (or refactor to avoid excessive context).
  - Use constrained prompts or structured outputs for extraction/classification instead.

---

Keep this card when deciding whether to enable extended thinking and how to handle its outputs.
