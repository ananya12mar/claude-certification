## Half-Written Tool Call — Revision Notes

- **Core problem:** appending a streamed assistant turn to history before the stream reached `message_stop` can commit a half-built `tool_use` block (truncated JSON), causing validation errors on the next request.

- **How it happens:** handler treats "read loop ended" as "message complete"; network blip or timeout ends stream mid-block (before `content_block_stop`), so partial JSON gets saved.

- **Fix (golden rule):** only append assembled assistant turns to history after `message_stop`. Do not parse or execute `tool_use` until its `content_block_stop` is received.

- **On interrupted streams:**
  - Discard partial assistant turns (do not write to history).
  - Retry the request from the last complete turn.
  - When debugging retries, check whether the prior turn was streamed.

- **Checklist:**
  - Buffer content deltas; finalize blocks only after `content_block_stop`.
  - Append turns to history only on `message_stop`.
  - On stream interruption, discard partial state and retry.
  - Add tests simulating mid-stream network failures to catch this early.

---

Keep this card handy when implementing streaming handlers and retry logic.
