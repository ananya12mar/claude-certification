## Streaming — Revision Notes

- **What streaming does:** sends response as events (partial message) so users see output sooner; you must reassemble blocks into a final message.

- **Core event types & handler actions:**
  - `message_start`: initialize empty content array.
  - `content_block_start`: reserve slot for block (`text`, `tool_use`, `thinking`) and index.
  - `content_block_delta`: append fragment to block (do not parse tool inputs yet).
  - `content_block_stop`: finalize block; only now parse tool JSON or run tool.
  - `message_delta`: record `stop_reason` and usage.
  - `message_stop`: stream finished — treat assembled message like non-streamed response.

- **Golden rule:** never act on a partial block — especially `tool_use`. Parse and execute only after `content_block_stop` and add assistant turns to history only after `message_stop`.

- **On interrupted streams:**
  - Treat partial turns as provisional; discard incomplete assistant turns (do not write to history).
  - Retry the request rather than committing partial state.
  - Check `stop_reason`: `tool_use` indicates tool calls are ready; other values mean a different flow.

- **When to use streaming:**
  - Long, user-facing responses where progressive display improves UX.
  - Avoid for short or backend-only calls to eliminate partial-state risk.

- **Checklist (implementation):**
  - Buffer deltas per block; parse only after `content_block_stop`.
  - Preserve full assembled turns when appending to history (only after `message_stop`).
  - Handle network/timeouts by discarding partial turns and retrying.
  - Monitor latency and output-length impact on UX and cost.

---

Keep this card when implementing streaming clients and handling partial outputs safely.
