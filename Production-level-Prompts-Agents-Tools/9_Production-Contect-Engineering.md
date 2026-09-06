## Production Postmortem — Revision Notes

- **Core issue:** sessions passed dev tests but hit context-budget cap in production because tool outputs grew much larger than test fixtures.

- **Measured difference:** dev fixture tool output ≈ 800 tokens; production tool output ≈ 3,200 tokens → window filled ~4× faster.

- **Failure mode:** accumulated tool results crowded out system prompts/instructions, causing wrong-tool choices and incomplete analyses around a fixed turn (e.g., turn 8).

- **Immediate fixes:**
  - Prune tool outputs after they are no longer needed.
  - Compact/summarize history proactively before reaching the budget cap.
  - Use `count_tokens` in prod to gate requests that would exceed budget.

- **Resilient design options:**
  - Persist large artifacts externally (DB, object store) and reference them rather than inlining.
  - Use subagents for self-contained subtasks and return concise summaries to parent.
  - Apply prompt caching for stable prefixes (system prompts, tool schemas).

- **Quick checklist (deploy readiness):**
  - Measure real tool-output token sizes using representative production samples.
  - Instrument token usage and alert when sessions approach budget thresholds.
  - Add compaction/pruning strategy and test mid- to long-horizon flows with large inputs.
  - Validate retry and error modes when context limits are reached (check `stop_reason`).

---

Keep this card when planning for production workloads that may exceed development fixtures.
