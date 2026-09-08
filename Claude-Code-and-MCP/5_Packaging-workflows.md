## Packaging Workflows — Revision Card

- The goal is to turn a working setup into something installable and shareable.
- You package the durable context, guardrails, and workflow logic so others can get the same setup in one step.

- Layers:
  - Skill: reusable workflow loaded on demand.
  - Custom command: explicit shortcut for a known procedure.
  - Plugin: bundled installable package of skills, hooks, agents, and MCP config.

- Skills
  - Live in .claude/skills as Markdown files.
  - Trigger by description match or explicit invocation.
  - Best for portable, task-specific procedures.
  - Must be runtime-safe: no local filesystem assumptions unless the runtime guarantees them.
  - Subagents do not inherit skills automatically.
  - In SDK usage, settingSources must be configured explicitly.

- Custom commands
  - Good for explicit, predictable entry points.
  - Skills are now the recommended format; legacy .claude/commands is older.
  - Namespaced by plugin; e.g. /payments:run-tests.

- Plugins
  - Bundle skills, hooks, subagents, and MCP servers.
  - Distributed via marketplace / installable as one unit.
  - Useful for sharing a setup across a team or org.
  - Managed settings can control allowed marketplaces and enterprise-level install priority.

- Design rules
  - Use skills for on-demand procedures.
  - Use CLAUDE.md for always-on project rules.
  - Use plugins when a setup must be versioned and shared.
  - Avoid hard-coded absolute paths or machine-specific assumptions.

- Cost / complexity / risk
  - Cost: skills add context load when activated; plugins add maintenance overhead.
  - Complexity: machine-specific assumptions break installs.
  - Risk: bundled guardrails do not carry over unless explicitly included.

Quick checklist

- Keep project-wide rules in CLAUDE.md
- Put reusable procedures in skills
- Use explicit commands for named workflows
- Bundle shared setups as a plugin
- Remove machine-specific paths before installation

### Q&A (flashcards)

1. **What is a skill?**  
   A reusable workflow loaded on demand.

2. **What is a custom command?**  
   A direct shortcut for a known task.

3. **When use a plugin?**  
   When a workflow must be shared, installed, and kept versioned across a team.

4. **What is the main portability rule for skills?**  
   Do not assume local filesystem or shell tools unless the runtime guarantees them.

5. **Why must settingSources be explicit in the SDK?**  
   Otherwise the skill may never load.

6. **What should live in CLAUDE.md instead of skills?**  
   Persistent project-wide rules that apply every session.

7. **What is the risk of a plugin?**  
   It includes only what is explicitly packaged; local guardrails can disappear if not bundled.

8. **One-line rule?**  
   Skills are portable procedures, commands are named entry points, and plugins are versioned team installs.
