## System Prompting — Revision Notes

- **Core idea:** Diagnose failure type first; add the single structural technique that fixes it. Don't just add words.

- **Four techniques (use as needed):**
  - **System prompt:** global behavioral contract — role, scope, rules.
  - **XML-style tags:** separate inputs, docs, and examples so boundaries are unambiguous.
  - **Few-shot examples:** show the exact input→output shape (use 1–3 targeted examples).
  - **Output constraints/schema:** specify exact form, field names, types, casing, and stop rules.

- **Diagnose → fix mapping:**
  - Wrong format → add output constraint (and examples/schema).
  - Scope drift → strengthen system prompt.
  - Correct task but wrong structure → add few-shot example(s).
  - Breaks on variants/edge cases → add constraints or example covering variant.

- **Worked example (classification):**
  - Problem: classifier returns inconsistent labels ("Billing" vs "billing" vs sentence).
  - Fix: system prompt + output constraint + few-shot examples wrapped in XML tags.
  - Result: deterministic label set (e.g., BILLING, TECHNICAL, ESCALATION) returned consistently.

- **Iteration rules:**
  - If re-prompting lengthens without fixing, stop and diagnose.
  - Apply a single structural fix, re-run, then re-diagnose if needed.

- **Quick checklist:**
  - Name the observed failure before editing the prompt.
  - Prefer minimal, targeted examples over long prose.
  - Use XML tags to isolate examples/inputs from instructions.
  - Lock formats with explicit constraints when machine-readability is required.

---

Keep this card for quick reference when hardening prompts for production.

## Structured outputs — Summary

- What: supply a JSON schema to the API so output is token-constrained to match it (constrained decoding).
- When to use:
  - `json_schema` for machine-readable responses your code consumes.
  - `strict` tool inputs to validate agent tool calls before execution.
- Why: prevents stray text, wrong field names, and removes parse-and-retry loops.
- Trade-offs:
  - First-call latency (schema compiles to a grammar; cached ~24h).
  - Slightly higher input token billing (injected schema prompt).
  - Not foolproof: `refusal` or `max_tokens` truncation can still produce non-matching output; always check `stop_reason`.
  - Incompatible with assistant message prefilling; choose one approach per request.

---

Use structured outputs when you need production-grade, machine-parseable reliability.
