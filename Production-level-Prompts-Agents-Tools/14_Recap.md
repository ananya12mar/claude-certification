## Recap — Revision Notes

1. Diagnose the failure before rewriting the prompt.

- Wrong shape = missing output constraints.
- Drift across turns = underspecified system prompt or memory.
- Hallucinated structure = missing few-shot examples.
- If inputs still break parsing, move control into structured outputs or strict tool schemas.

2. Match reasoning depth to the task.

- Enable reasoning only when it changes the answer.
- Tune effort and model choice to the task, not to a default.
- Reasoning is a tool, not a universal fix.

3. A stream ending is not a completed message.

- Wait for block close and message_stop before acting.
- Only commit successful turns to history.
- If a stream is interrupted, discard the partial turn and retry.

4. Wrong-tool calls usually come from schema design.

- Claude matches tool descriptions to the request.
- Add exclusion conditions like “don’t call this when…”.
- MCP helps, but every connected tool adds context cost.

5. Context is a fixed budget; tool outputs spend it fast.

- Production outputs are much larger than dev fixtures.
- If performance degrades after N turns, inspect window management first.
- Prune, compact, or hand off to subagents when needed.

6. Workflow vs agent is a product decision.

- Workflow when the path is known.
- Agent when the goal is known but the path is not.
- Put human checkpoints before irreversible actions.

7. Memory should fit the session shape.

- In-context memory is simplest but breaks in short, repeated sessions.
- External storage improves persistence; summaries save cost but lose detail.
- Stateless is correct for bounded tasks.
- Skills carry reusable instructions without polluting every session.

8. Multimodal inputs have real cost and latency tradeoffs.

- Image tokens scale with resolution.
- Test against production-size inputs, not only dev samples.
- Use Files API for shared assets and Batches API for offline work.
- Do not treat a synchronous loop as batching.

### Quick checklist

- Diagnose the failure type first
- Add the missing technique, not more wording
- Tune reasoning and model to the task
- Treat stream completion as explicit state
- Design tool descriptions and exclusions carefully
- Manage the context window proactively
- Choose workflow vs agent deliberately
- Decide memory and multimodal cost upfront
