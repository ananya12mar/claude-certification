## What Sent Claude To The Wrong Tool — Revision Notes

- **Core problem:** overlapping descriptions confuse Claude; similar-sounding tool descriptions give no reliable decision signal.

- **Diagnostic clue:** Claude repeatedly calls the wrong tool for inputs near the boundary between tools (e.g., calls `search_docs` even when answer exists in session).

- **Simple fix:** add exclusion conditions — one sentence saying _when not to use_ the tool.
  - Example: `search_docs`: "Use this to look up content not already present in the current session. Do not call this if the answer is available in session context."
  - Mirror with the complementary tool: `get_context_summary`: "Only use this if the answer is present in the current session. Do not use to look up new information."

- **If exclusions fail:** merge similar tools into one with a type parameter, or redesign interfaces to avoid overlap.

- **Checklist:**
  - Check descriptions for overlapping language ("find information").
  - Add explicit exclusion sentences to create decision boundaries.
  - Re-run tests near boundary cases; if misroutes persist, consider merging tools.

---

Keep this card handy when debugging wrong-tool selections.
