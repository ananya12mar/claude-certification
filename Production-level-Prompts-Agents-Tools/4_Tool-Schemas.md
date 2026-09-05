## Tool Schemas — Revision Notes

- **Core idea:** Claude chooses tools based on your schema. Good schemas + correct block handling = reliable tool-use.

- **Tool-use loop (simplified):**
  1.  Define schema (name, description, input_schema)

2.  Send message
3.  Assistant emits `tool_use` block (tool name, id, args)
4.  App executes tool and returns `tool_result` with matching id
5.  Claude continues using the result

- **Message block rules (must follow exactly):**
  - `text` block: Claude prose — preserve it when appending history.
  - `tool_use` block: contains tool name, unique `id`, and args — must be answered immediately.
  - `tool_result` block: user turn returns matching `tool_use` id and result (optional `is_error`).
  - `thinking` block: internal reasoning (extended thinking) — must be returned unchanged (signature-verified).
  - Invariant: every `tool_use` in an assistant turn must have a matching `tool_result` in the immediately following user turn.

- **Schema anatomy (what Claude reads):**
  - `name`: concise, specific identifier (e.g., `get_account_balance`).
  - `description`: 3–4 clear sentences: what it does, when to use it, when not to. Include input examples if format matters.
  - `input_schema`: JSON Schema with required/optional fields. Mark only truly required fields as `required`.

- **Design decisions that matter:**
  - Subtask dependency: sequence vs parallel calls (use `disable_parallel_tool_use` to force serial).
  - Required vs optional fields: over-requiring forces fabricated values.
  - Overlapping parameter types: disambiguate via descriptions or merge tools with a type parameter.
  - Description length: be concise but specific — too short → guesses; too long → buried triggers.

- **MCP (Model Context Protocol) notes:**
  - Use MCP servers when well-maintained tool catalogs exist (e.g., GitHub integrations).
  - MCP tools are treated identically by Claude; the difference is who authored the schemas.
  - MCP servers add definitions to context; register only needed servers and use `mcp_toolset` to control loading.
  - `defer_loading` delays loading tool defs until needed; `enabled` toggles specific tools.
  - Transports: local (stdio) or remote (Streamable HTTP + optional SSE). API MCP Connector supports only HTTP servers.

- **Practical checklist:**
  - Write clear descriptions with exclusion conditions.
  - Mark only necessary `required` fields.
  - Prefer merging similar tools rather than long disambiguating prose.
  - Preserve `text`, `tool_use`, `tool_result`, and `thinking` block pairing exactly.
  - Measure context cost when connecting MCP servers; use defer/loading controls.

---

Keep this card when designing schemas or integrating MCP servers.
