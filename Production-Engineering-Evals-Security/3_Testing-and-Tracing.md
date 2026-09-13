# Testing and Tracing

## Problem

A good eval score tells you the system is working on average, but not where a failure happened.

## Why it matters

- A passing eval can hide a broken step in the workflow.
- Different test levels catch different failure modes.
- Traces help you localize the exact point of failure.

## Test levels

- Unit test: isolates one function, such as a parser or tool wrapper.
- Functional test: checks one model call returns the expected shape.
- Integration test: validates the handoff between components.
- End-to-end test: checks the full user flow from input to output.

## Why tracing matters

- Tests tell you a failure exists.
- Traces show which step produced the bad result.
- Without a trace, debugging turns into slow manual investigation.

## Example

- Query: "Where is my refund?"
- Step 4 parser fails with KeyError: amount
- The trace shows the model output was returned, but the parser broke on a missing field

## What to do

- Add tests at each layer.
- Match each test to the failure it can isolate.
- Log prompts, tool calls, intermediate outputs, and timing.
- Use traces to debug regressions and review changes.

## Takeaway

The eval measures outcome. Tests and tracing explain the failure.

Together they make the system debuggable, reviewable, and easier to improve.
