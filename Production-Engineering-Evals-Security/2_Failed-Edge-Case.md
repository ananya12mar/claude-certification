# Failed Edge Case

## Problem

A feature can look correct in demos while still extracting the wrong value.

## Why it matters

- A model can sound convincing and still be wrong.
- Validation checks shape, not correctness.
- Real-world inputs often include edge cases that happy-path examples miss.

## Example failure

Customer message: "I placed my order on March 3 but did not receive it until April 12."

- System extracted: "April 12"
- Correct value: "March 3"
- Both dates were valid.
- The field was populated.
- Validation still passed.

## Root cause

- The team tested only single-date examples.
- They had not defined expected behavior for multi-date inputs.
- There was no graded set or holdout set.
- The failure was not in the model or prompt alone; it was in the missing eval.

## What to do

- List likely edge cases.
- Turn them into graded examples with human-checked expected outputs.
- Include cases like:
  - two dates in one sentence
  - no date at all
  - relative dates such as "next Tuesday"
- Re-run the eval after every change.

## Takeaway

Validation confirms that a value is in the right format. It does not confirm that it is the right value.

The eval is what catches this failure and prevents it from returning in production.
