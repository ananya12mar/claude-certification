## CLAUDE.md That Kept Growing — Revision Card

- The failure mode is not “missing rules”; it is rule dilution.
- A long CLAUDE.md keeps every instruction in context, but it reduces the effective weight of the important ones.

- Setup:
  - CLAUDE.md grew from reasonable additions over time.
  - It reached 800+ lines with framework rules, style guides, historical notes, and archived content mixed together.

- The problem:
  - The rule “do not touch /legacy/tokens/” was present, but it got buried.
  - The agent still had access to it, but the important instruction was diluted by 846 other lines.

- What belongs in CLAUDE.md:
  - Global constraints
  - test commands
  - framework conventions
  - “never touch” rules

- What does not belong:
  - historical decisions log
  - archived notes
  - path-specific guidance that should be scoped elsewhere
  - reference material that is not session-critical

- Better structure:
  - CLAUDE.md = short, high-signal operating rules
  - .claude/rules/ = path-specific instructions
  - separate docs = reference/history material
  - hooks = enforcement when model compliance is not enough

- Rule of thumb:
  - If it changes behavior, keep it near the top.
  - If it is reference-only, move it out of the session default context.

Quick checklist

- Keep CLAUDE.md under a few hundred lines if possible
- Put path-specific rules in .claude/rules/
- Move history and archives out of the active rules file
- Keep the highest-priority safety instructions short and visible
- Audit for dilution when the file keeps growing

### Q&A (flashcards)

1. **What was the main failure?**  
   Rule dilution, not missing information.

2. **Why did the important rule get ignored?**  
   It was buried in a very large CLAUDE.md.

3. **What should live in CLAUDE.md?**  
   Core project rules that change behavior every session.

4. **What should not live there?**  
   History, archives, and path-specific guidance better handled elsewhere.

5. **Where should path-specific rules go?**  
   In .claude/rules/ with paths scoping.

6. **What is the best design principle?**  
   Keep the active instructions short, relevant, and high-signal.

7. **What is the “one rule you cannot afford to dilute”?**  
   The safety or blocking rule that prevents a real mistake.

8. **One-line rule?**  
   CLAUDE.md is a working rule set, not a project archive; if a rule is not session-critical, it should not live there.
