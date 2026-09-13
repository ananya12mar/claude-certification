# Broken Seam

## Problem

Each component passed its own tests, but the system still failed at the handoff.

## Why it matters

- Unit and functional tests can both pass while the full flow fails.
- The most common production break is at the seam between components.
- A contract mismatch can look fine in isolation and still break end-to-end.

## Example failure

- Retrieval returns a list of dictionaries
- Prompt builder expects a plain string
- Model receives malformed context and answers from memory

## Root cause

- The format contract between steps was never defined.
- No integration test exercised the retrieval-to-model handoff.
- Each side was correct on its own, but not together.

## What to do

- Add integration tests for real component handoffs.
- Define clear input/output contracts at every boundary.
- Validate the data that moves between steps, not just the steps alone.

## Takeaway

A system is only as strong as its seams.

The eval catches the outcome. The integration test catches the mismatch before users do.
