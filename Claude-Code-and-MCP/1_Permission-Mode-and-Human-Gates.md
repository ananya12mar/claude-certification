## Permission Modes + Human Gates — Revision Card

- Claude Code follows an explore → plan → code loop.
- The permission mode decides how often the agent pauses for approval.
- The review gate decides when a human must inspect before an action is allowed.

- Core idea:
  - Low-risk, reversible actions can be auto-approved.
  - High-risk, hard-to-reverse actions should require human review.

- Permission modes:
  - Default: read-only auto; prompts before edits/commands.
  - acceptEdits: auto-approves local edits and common filesystem actions in working dir.
  - Plan: reads only; no writes until plan is approved.
  - Auto: broad autonomy with safety classifier; still blocks dangerous actions.
  - Dont Ask: only allow-listed tools; denies everything else.
  - ByPassPermissions: no prompts, no safety checks; only for disposable isolated environments.

- Settings scope:
  - User level: personal defaults.
  - Project level: repo-wide team rules.
  - Local project level: personal override, not committed.
  - Enterprise level: org-wide controls; strongest enforcement.

- Rule precedence:
  - Deny rules beat allow rules.
  - Enterprise deny rules are the hardest control to override.

- Human gate placement:
  - Ask: what is the worst-case cost if this runs unchecked?
  - Low cost → allow more automation.
  - High cost / hard to undo → require a human gate.

- Best practice:
  - Use Plan or Default on unfamiliar/sensitive work.
  - Use acceptEdits on trusted local edits.
  - Keep bypass modes isolated and rare.
  - Treat sensitive code changes as human-reviewed, not agent-approved.

Quick checklist

- Choose mode based on risk and reversibility
- Keep defaults safe on unfamiliar repos
- Use project/enterprise deny rules for real guardrails
- Put human gates on destructive or high-cost actions
- Never rely on a bypass mode on a live developer machine

### Q&A (flashcards)

1. **What is the Claude Code loop?**  
   Explore → plan → code.

2. **What does Plan mode do?**  
   It blocks edits and shell commands until the plan is approved.

3. **When is acceptEdits appropriate?**  
   On trusted local work where small edits are safe and reversible.

4. **When should a human gate be required?**  
   When the action is hard to undo, sensitive, or high impact.

5. **What wins: allow or deny?**  
   Deny always wins.

6. **What is the strongest settings layer?**  
   Enterprise-level managed rules.

7. **Why is ByPassPermissions dangerous?**  
   It disables prompts and safety checks; only safe in disposable isolated environments.

8. **One-line rule?**  
   Use the least permissive mode that still gets the job done, and place human gates where the cost of a mistake is too high to trust automation.

Keep this as your permission-governance cheat sheet.
