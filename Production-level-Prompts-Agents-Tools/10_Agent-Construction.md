## Agent Construction — Revision Card (concise)

- Decision: Workflow = fixed/enumerable steps; Agent = dynamic tool sequencing.
- Wiring paths: Raw Messages API (full control) · Agent SDK (local loop) · Managed Agents (Anthropic-run; stateful).
- Core loop (4): Register tools → Scope system prompt → Execute tool-use & return results → Explicit exit.
- HITL: before destructive writes/sends; after planning; on unexpected/error outputs.
- Tools: minimal, orthogonal, clearly described; add only for confirmed gaps.
- Compliance: name PHI/GDPR/FedRAMP early — determines endpoint, creds, and logging.

Quick checklist

- Tools registered
- System prompt scoped to task & tools
- Tool-use loop implemented and tested
- HITL gates added for high-risk steps
- Explicit exit conditions

---

### Q&A (flashcards)

1. **When pick workflow vs agent?**  
   Workflow = enumerable fixed steps; Agent = dynamic sequencing over tools.

2. **Wiring paths?**  
   Raw Messages API; Agent SDK; Managed Agents (Anthropic-run loop/sandbox).

3. **Core loop steps?**  
   Register tools → Scope prompt → Execute tool-use (return tool-result) → Stop on exit.

4. **System prompt rule?**  
   Scope to the task and list only available tools; avoid describing unregistered tools.

5. **When add HITL?**  
   Before destructive actions; after planning; on unexpected/error outputs.

6. **Tool registration guidance?**  
   Keep tools minimal and orthogonal; overlapping descriptions harm routing.

7. **When use Managed Agents?**  
   For long-running sessions or when you want a managed sandbox — only if compliance allows stateful sessions.

8. **What does compliance change?**  
   Endpoint choice, credentialing, logging/retention, and allowed deployment routes.

9. **Common production failures?**  
   Over-tooling, vague prompts, missing HITL, undefined exit criteria, and untested long runs.

10. **One-line prod checklist?**  
    Tools registered; prompt scoped; loop implemented; HITL gates; exit defined.

Keep this file as your one-page revision card for agent design.
