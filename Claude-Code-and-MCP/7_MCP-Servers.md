## MCP Servers — Revision Card

- An MCP server exposes tools, resources, and prompts to Claude from outside the app code.
- It turns one integration into a reusable capability for many clients.

- Core concepts:
  - Tool: action the model can call.
  - Resource: read-only data fetched into context.
  - Prompt: reusable instruction template.

- Transport:
  - stdio: local process; good for local tools.
  - HTTP: remote hosted service; common for shared servers.
  - SSE: legacy; avoid for new work.

- Scope:
  - Local: personal project-only setup.
  - User: personal across all projects.
  - Project: committed .mcp.json for team use.
  - Enterprise: admin-managed shared deployment.

- Context cost:
  - Every connected MCP server adds tool definitions to the context pool.
  - Claude should load only relevant tools, not all server tools at once.

- Prompt caching:
  - Useful for stable prefixes like tool definitions or long prompts.
  - Cache works only when content matches exactly.
  - Default lifetime is ~5 minutes; TTL can extend to 1h.

- RAG vs agentic search:
  - Classical RAG: index first, then retrieve by similarity.
  - Agentic search: search on demand during the task.
  - Both aim to fetch only the relevant slice, not the whole library.

- Server governance:
  - Scope permissions to individual tools, not just the whole server.
  - Example: allow one GitHub tool, deny a write-capable one.

- GitHub server example:
  - HTTP transport
  - project or local scope depending on team access
  - PAT stored in env var, never committed in .mcp.json
  - OAuth is different: browser-based sign-in flow for user identity

- Secret rule:
  - never commit API keys into repo config
  - keep them in env vars or managed secret stores

Quick checklist

- Choose transport based on where the server runs
- Choose scope based on who should access it
- Keep only needed servers connected
- Store secrets in env vars, not config files
- Restrict permissions to specific tools where possible

### Q&A (flashcards)

1. **What is an MCP server?**  
   A reusable process that exposes tools/resources/prompts to clients.

2. **What is the difference between a tool and a resource?**  
   A tool performs an action; a resource provides read-only context.

3. **What transport is used for a remote shared server?**  
   HTTP.

4. **When is stdio appropriate?**  
   For a local tool running on the user’s machine.

5. **Why is scope important?**  
   It decides who can use the server and where config lives.

6. **What is the biggest secret risk?**  
   Committing API keys in .mcp.json.

7. **What should you do with MCP tool permissions?**  
   Allow or deny specific tools, not just the entire server.

8. **One-line rule?**  
   Keep MCP servers lean, scoped, and secret-safe; only expose the tool surface the task actually needs.
