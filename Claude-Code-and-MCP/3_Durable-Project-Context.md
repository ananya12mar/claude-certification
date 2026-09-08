## Durable Project Context — Revision Card

- This is about how project knowledge survives across sessions.
- The goal: keep rules available without stuffing every session with noisy context.

- Core mechanisms:
  - CLAUDE.md: always loaded at session start; best for global project rules.
  - Rules files: path-scoped guidance; loaded only when relevant.
  - Hooks: enforce actions at lifecycle events; not just model intent.
  - Subagents: isolated workers with their own context and smaller blast radius.

- CLAUDE.md
  - Loaded every session automatically.
  - Best for universal constraints, test commands, framework rules, and “never touch” paths.
  - Risk: grows too large and dilutes the important rules.
  - Keep it tight; move lower-priority detail to Skills.

- Rules files
  - Live under .claude/rules/
  - Use YAML frontmatter with paths to scope them.
  - Good for directory-specific rules like database or frontend conventions.
  - Unscoped rules behave like CLAUDE.md and load at startup.

- Hooks
  - Trigger at lifecycle moments: PreToolUse, PostToolUse, SessionStart, SessionEnd, etc.
  - Great for guardrails, formatting, audits, and follow-up actions.
  - PreToolUse can block dangerous calls before they happen.

- Subagents
  - Delegate work into an isolated context.
  - They do not inherit the main session state.
  - Explore/Plan subagents skip some project context to stay fast.
  - For strict project rules, use the general-purpose or custom subagent with required skills.

- Rule of thumb:
  - Global invariant → CLAUDE.md
  - Local rule → path-scoped rules file
  - Repeated action → hook
  - Isolated research / separate task → subagent

Quick checklist

- Keep CLAUDE.md small and high-signal
- Put path-specific instructions in .claude/rules/ with paths
- Use hooks for enforcement that should happen no matter what the model decides
- Use subagents when isolation helps or context would bloat the main session
- Only add project context that changes behavior

### Q&A (flashcards)

1. **What loads in every session?**  
   CLAUDE.md.

2. **What belongs in CLAUDE.md?**  
   Global project rules, commands, and non-negotiable constraints.

3. **What does a rules file do?**  
   Adds path-scoped instructions only when relevant.

4. **When is a hook better than a rule?**  
   When you need enforcement regardless of model intent.

5. **What is the key difference between a hook and a rule?**  
   A hook runs automatically at the lifecycle event; a rule depends on model behavior.

6. **Why use subagents?**  
   To isolate work and reduce main-session context bloat.

7. **What is the risk of a bloated CLAUDE.md?**  
   It dilutes important instructions and consumes valuable context.

8. **One-line summary?**  
   Put invariant project knowledge in CLAUDE.md, local guidance in scoped rules, enforcement in hooks, and delegated tasks in subagents.
