# How LLMs Work — Revision Notes

- **Tokens — unit of I/O & cost:**
  - Models operate on tokens, not raw characters; chars-per-token varies by tokenizer.
  - Everything counts: system prompt, conversation history, tool defs/results, and output.
  - Practical: estimate costs and limits in tokens; verify tokenizer at build time.

- **Context window — fixed token budget:**
  - Contains full request: prompts, history, docs, tool results, and model output.
  - If input > window → request rejected; if exceeded during generation → model stops (model_context_window_exceeded).
  - Mitigations: trim/summarize history, chunk documents, or stream outputs.

- **Sampling — source of variability:**
  - At each step the model produces a probability distribution and samples a token.
  - Lower temperature = more repeatable; higher = more varied. Some models ignore sampling params and require prompt steering.
  - Check model docs for supported sampling controls.

- **Non-determinism — testing implications:**
  - Don't assert exact text. Assert properties: presence, type, ranges, parseability.
  - Use model-graded evaluations for meaning-level correctness.

- **Quick checklist (build & tests):**
  - Confirm tokenizer behavior and typical chars-per-token.
  - Monitor token usage and billing.
  - Implement history trimming/summarization and chunking strategies.
  - Design tests to assert properties, not verbatim outputs; use evals for semantics.

---

Keep this short card handy when designing prompts, budgeting context, or writing tests.
