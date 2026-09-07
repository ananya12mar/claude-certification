## Window-Filled — Revision Card

- Dev vs prod mismatch:
  - Dev: one long session; context never fills.
  - Prod: many short sessions across days; memory accumulates.
  - Result: by session four, history alone can exceed the usable context budget.

- Root cause:
  - In-context memory was treated as if it were durable state.
  - Full session history, system prompt, and tool schemas were all injected every turn.
  - The real failure was context exhaustion, not bad tool selection.

- Why it looked like a tool problem:
  - Agent returned incomplete outputs just before budgeting failed.
  - The error surfaced late, after too much history had already been loaded.

- The fix:
  - Move long-lived state out of live context.
  - Store relevant history in external storage.
  - Inject only a filtered subset at session start.

- Design rule:
  - Measure token usage per session before choosing in-context memory as the default.
  - In-context is cheap and easy, but it breaks once state grows across sessions.

- Practical guidance:
  - Short-lived task state: keep in-context.
  - Ongoing user case / multi-session memory: use DB or summarized memory.
  - Test at session boundaries, not only in a single long test run.

Quick checklist

- Measure token budget with history + system prompt + tool schemas
- Separate in-context state from durable state
- Persist long-running session memory externally
- Retrieve only the relevant slice at session start
- Validate against realistic multi-session production load

### Q&A (flashcards)

1. **Why did dev work but prod fail?**  
   Dev used one continuous session; prod used repeated sessions with accumulated state.

2. **What was the real issue?**  
   Context window exhaustion caused by oversized in-context memory.

3. **Why did it look like a tool failure?**  
   The agent failed only after too much history had already consumed the context budget.

4. **What was the fix?**  
   External storage + selective retrieval of only relevant history.

5. **When is in-context memory okay?**  
   Only for short-lived sessions where the full state fits comfortably.

6. **What should be measured before shipping?**  
   Actual token usage across session boundaries and realistic production patterns.

7. **Design one-liner?**  
   Decide memory scope before deployment; keep active state short and durable state external.

Keep this as your one-page rule: memory that must survive sessions should not live in the live context window.
