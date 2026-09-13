## Claude Code + MCP Recap — Revision Card

- Permission mode is a risk decision, not a convenience setting.
- Durable context needs the right mechanism for each job.
- Shared workflows must be portable, not machine-specific.
- Enterprise integrations require security design before production.

1. **Permission mode**
   - match the mode to risk, not just speed
   - bypass on a live repo is dangerous
   - deny rules are the real safety net

2. **AI review**
   - trust only what the diff can prove
   - treat unverified runtime claims as hypotheses
   - put the human gate where undo is expensive

3. **Skills**
   - portable, but only if runtime assumptions are explicit
   - subagents do not inherit skills automatically
   - local filesystem assumptions break across runtimes

4. **Durable context**
   - CLAUDE.md = always-on project defaults
   - rules files = path-scoped guidance
   - hooks = deterministic enforcement
   - subagents = isolated work

5. **Packaging shared workflows**
   - use relative paths and root-aware variables
   - document required env vars
   - test on a clean machine before distribution

6. **MCP transport + scope**
   - stdio = local
   - HTTP = remote/shared
   - local/user/project/enterprise scope = different sharing levels
   - match the transport and scope to deployment intent

7. **Enterprise security**
   - OAuth for user identity
   - env vars / secret store for service credentials
   - PostToolUse hooks for audit
   - managed settings for locked config

Quick checklist

- Match mode to risk
- Keep CLAUDE.md short and high-signal
- Use scoped rules, hooks, and subagents appropriately
- Test plugins on clean machines
- Keep secrets out of repo config
- Verify OAuth registration for each environment
- Add audit and governance for production systems

### Q&A (flashcards)

1. **What is the main idea of permission modes?**  
   They are risk controls, not speed preferences.

2. **What should CLAUDE.md contain?**  
   Only the rules that change behavior every session.

3. **What is the role of hooks?**  
   Deterministic enforcement and automation.

4. **Why do shared plugins fail?**  
   Because of machine-specific paths or undocumented env vars.

5. **What is the difference between stdio and HTTP?**  
   stdio is local; HTTP is for remote/shared services.

6. **What is the big enterprise security rule?**  
   Secrets stay out of committed config and audit controls are required.

7. **What should be tested before prod?**  
   OAuth registration, environment config, and real production sign-in paths.

8. **One-line summary?**  
   The module is about engineering agent behavior safely: the right permissions, the right context, the right packaging, and the right security controls.
