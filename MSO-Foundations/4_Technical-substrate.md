## Technical Substrate — Revision Notes

- **Access: REST API vs SDKs:**
  - Core API is HTTP REST; SDKs (Python, TypeScript, etc.) are thin wrappers for auth, retries, and parsing.
  - SDK and raw REST hit the same endpoints; prefer SDKs to reduce boilerplate.
  - Module 2 uses the SDK Messages API—confirm client and endpoints at build time.

- **Response modes:**
  - **Synchronous:** send request, wait for full JSON response — simple, good for short/backend jobs.
  - **Streaming:** server-sent events over HTTP; receive partial output as it’s generated; assemble and render progressively.
  - **Practical:** use streaming for long user-facing outputs; implement reassembly and interruption recovery.

- **Async & high-volume patterns:**
  - **Async clients:** Python has an async client; TypeScript clients are Promise-based — use for non-blocking concurrency.
  - **Batch API:** submit large sets, receive job id, poll for results; lower per-token cost, up to ~24h latency — ideal for offline pipelines and large evals.

- **Quick checklist:**
  - Use SDKs for convenience and correct defaults.
  - Choose streaming for UX-sensitive, long outputs; handle stream errors/reconnects.
  - Use async patterns for concurrency; use Batch API for cost-sensitive bulk jobs.

---

Keep this as a compact reference when implementing API calls, streaming clients, and bulk workflows.
