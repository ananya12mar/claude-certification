## Agent Memory — Revision Card

- Memory scope: decide at design time what must survive sessions vs what stays in-context.

- Memory types (one-line):
  - In-context: lives in the active conversation; cheap to implement; inflates token cost; short sessions only.
  - External storage: durable DB reads/writes; survives restarts; adds latency and engineering work.
  - Summarized memory: compressed history injected at session start; lower tokens but lossy.
  - Stateless: no persistence; use for single-run jobs or isolated pipelines.

- Tradeoffs: too much in-context → token/latency explosion; too little persistence → lost continuity.

- Practical guidance:
  - Pick scope during design, not during a late refactor.
  - Prototype in-context, plan for external/summarized migration as sessions grow.
  - Measure real session token usage before committing to an in-context strategy.

- Skills vs CLAUDE.md vs in-context instructions:
  - Skill (SKILL.md): loads on-demand when request matches; low startup cost; task-specific.
  - CLAUDE.md: loads every session; fixed overhead; use for global project standards.
  - In-context: present every turn; does not survive sessions; use for short interactions.

Quick checklist

- Name memory scope in design docs
- Implement minimal external schema for persistent state
- Add summarization only when needed and test lossy cases
- Register Skills for repeatable task instructions
- Add retrieval latency and privacy checks to design

---

### Q&A (flashcards)

1. **What are the four memory types?**  
   In-context, External storage, Summarized memory, Stateless.

2. **When use in-context memory?**  
   Short sessions where full state fits within context window.

3. **Why use external storage?**  
   To persist state across sessions, share between agents, or move state between users.

4. **When is summarized memory useful?**  
   Long-running chat where full history would exceed context budget; accept lossy summaries.

5. **What is a Skill (SKILL.md)?**  
   Reusable instruction set that loads on demand when a request matches its description.

6. **CLAUDE.md vs Skill — difference?**  
   CLAUDE.md loads every session (always-on); Skill loads only on match (on-demand).

7. **What to measure before committing to in-context?**  
   Actual token usage per session and how it grows with turns.

8. **Design checklist one-liner?**  
   Decide scope → persist minimal state → add summarization → register Skills → test long runs.

Keep this as your one-page memory design checklist.
