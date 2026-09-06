## Context Engineering — Revision Notes

- **Big picture:** pick the right model, then manage the context window. Model choice sets cost/latency/capability; context engineering decides what stays in working memory.

- **Model selection (practical):**
  - Start with `Sonnet` (balanced). Move to `Opus` only if evals show a quality gap; move down to `Haiku` only when quality tradeoffs are acceptable.

- **Context window basics:**
  - Every prompt, tool result, doc, and assistant reply consumes tokens in the window.
  - Input > window → validation error; generation that hits the ceiling → `model_context_window_exceeded` stop reason.
  - Production fills the window faster than tests (longer tool outputs, more turns).

- **Four strategies to stay in budget:**
  - **Pruning:** rewind and drop later turns; simple but loses intermediate work.
  - **Compaction (summarize):** condense history to preserve key facts at lower token cost; risk: lost details unless summarizer prompt is precise.
  - **Clearing (new session):** start fresh when context would bias or confuse; persistent state must be stored externally.
  - **Subagent handoffs:** spawn isolated subagents for subtasks and return concise summaries to parent; keeps main context small.

- **Cost-reduction levers:**
  - **Prompt caching:** cache stable request prefixes (system prompt, tool schemas) via `cache_control` to reduce reprocessing cost.
  - **Token counting:** use `count_tokens` to gate requests before hitting the window.

- **RAG pipeline pitfalls (three breakpoints):**
  1.  **Chunking:** choose chunk size (sentence/section with overlap) to balance context and retrieval.

2.  **Embedding match:** semantic search may miss exact identifiers—combine with lexical matching when needed.
3.  **Assembly:** retrieved chunks must be presented in the prompt structure the model expects.
    - For stable corpora, own an index; for changing sources, iterative search may be simpler despite higher per-query cost.

- **Compaction & subagents (practical):**
  - Manual summarizers must be explicit about what to preserve (file paths, decisions, errors).
  - Subagents receive minimal context, tools, and clear exit criteria; parent aggregates results.

- **Quick checklist:**
  - Start with `Sonnet` and validate with evals before switching models.
  - Instrument token counts in dev and prod; monitor real tool-output sizes.
  - Use compaction only with precise summarizer prompts.
  - Use subagents for self-contained subtasks; add tests for long-horizon flows.

---

Keep this card when designing multi-turn agents and scaling long-running sessions.
