# Tool Errors

## Problem

Production failures are not all the same. A retry that helps for one error can make another worse.

## Why it matters

- Rate limits and malformed requests are different failure types.
- Retrying a terminal error wastes time and budget.
- Dropping tool errors silently turns a failure into bad output.

## Classify the failure

- Retriable: rate limit, overload, temporary server issue, timeout
- Terminal: bad request, auth failure, permission issue, invalid input

## What to do

- Check the status code before retrying.
- Honor retry-after when present.
- Avoid stacking retry loops from both app code and the SDK.
- Treat an unknown failure as terminal unless you are confident it is transient.

## Tool output handling

When a tool fails, return the error to Claude with is_error set to true.

- Do not silently return an empty result.
- A visible failure lets the model react.
- A hidden failure produces a confident but wrong answer.

## Example

- 429 or 529: retry with backoff
- 400 or 401: fail fast
- 200 with refusal: raise and log; do not retry blindly

## Takeaway

The system should handle failure by type, not by hope.

Retry only when time is likely to fix the problem. Otherwise fail loudly and surface the error.
