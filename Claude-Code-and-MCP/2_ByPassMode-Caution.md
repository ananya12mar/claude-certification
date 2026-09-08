## ByPassPermissions — Revision Card

- The danger is not “obvious dangerous commands”; it is the silent prompt removal that lets a broad action run unchecked.
- The agent looked safe because the task felt routine, but the pattern matched files outside the intended scope.

- Key lesson:
  - bypassPermissions disables the exact safety checkpoint that would have stopped the script.
  - A broad match + no prompt = destructive action with no human brake.

- Important nuance:
  - The risky gate was the script invocation, not necessarily the final rm call.
  - acceptEdits still auto-approves common local filesystem actions; default mode is the one that prompts for them.

- What broke here:
  - The cleanup script searched /v1/legacy/
  - It matched both /src/ and /deploy/config/prod/
  - The environment-specific production config was deleted

- What to watch:
  - broad file patterns
  - cleanup scripts
  - destructive shell commands
  - sensitive directories outside the working scope

- Safety rule:
  - If you want fewer prompts without losing protection, prefer classifier-gated modes like Auto over a full bypass.
  - Add deny rules for sensitive paths before switching modes.

Quick checklist

- Never assume a “small” task is safe in bypass mode
- Check path scope before running scripts
- Add deny rules for sensitive directories
- Prefer Auto over full bypass when you need less friction
- Treat script execution as a human-gated action when scope is uncertain

### Q&A (flashcards)

1. **Why was the task dangerous?**  
   The agent matched a broader file set than intended and ran a script without a prompt.

2. **What did bypassPermissions remove?**  
   The confirmation step that would have stopped the unsafe cleanup.

3. **Was it the rm command itself that mattered?**  
   Not necessarily. The prompt was lost before the script reached the destructive step.

4. **What is the safer alternative?**  
   Use a classifier-gated mode such as Auto or keep a deny rule on sensitive paths.

5. **Why did the production config get deleted?**  
   The search pattern matched both app files and deploy config files.

6. **What should you protect in config?**  
   Sensitive directories such as deployment, environment, or production config paths.

7. **One-line rule?**  
   A bypass mode is only safe in isolated disposable environments; on real repos it removes the very prompt that prevents accidental destruction.
