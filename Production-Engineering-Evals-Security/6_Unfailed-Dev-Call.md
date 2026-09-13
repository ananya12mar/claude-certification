# Unfailed Dev Call

## Problem

A call that never fails in development can still fail in production.

## Why it matters

- Development traffic is too light to trigger many production failures.
- Low-volume runs hide rate limits, timeouts, and transient errors.
- If no error path exists, the first real failure becomes an outage.

## Example failure

A batch job calls the API in a loop.

- Development: all calls succeed
- Production: rate limit hits
- Result: unhandled exception and the whole request fails

## Root cause

- The code assumed every call would return successfully.
- No retry or backoff path was implemented.
- A naive retry loop made the problem worse by increasing load.

## What to do

- Treat failures as part of production behavior, not edge cases.
- Classify errors as retriable or terminal.
- Add exponential backoff with a cap and honor retry-after when present.
- Write the error path before shipping.

## Takeaway

The failure that never appears in dev is often the one that breaks production.

Handle retriable errors with backoff, not panic and not hammering retries.
