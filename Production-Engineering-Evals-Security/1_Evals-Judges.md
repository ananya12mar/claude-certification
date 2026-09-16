# Evals & Judges — Revision Notes

## 1 Design doc first

- Before coding, write a short design doc with:
  - success criteria
  - failure handling
  - cost/latency budget
  - trust boundary
- This defines what “correct” means before the model produces output.
- It keeps system parts aligned: evals, error handling, budget, security.

## 2 Eval = measurable quality

- An eval is a fixed set of test cases + expected outputs.
- Run feature on each case, grade result, average score.
- This turns “looks right” into a trackable metric.
- Good evals catch regressions and show what changed when score moves.

### Minimal pattern

- `run_test_case(test_case)` -> run model + grade output
- `run_eval(dataset)` -> run all cases and average scores

### Rule

- Change one variable at a time: prompt, tools, or model.
- Measure per-case failures, not just average score.
- A high average can hide a bad tradeoff.

## 3 Grading methods

### Exact match / string match

- Best for single correct answer.
- Very cheap, very brittle.
- Fails valid paraphrases or reordered outputs.

### Code-graded checks

- Best for structured outputs.
- Validate JSON, Python syntax, required fields, numeric ranges.
- Cheap and reliable for format/structure.

### LLM-as-judge

- Best for open-ended quality.
- Use when output quality depends on faithfulness, completeness, instruction following.
- Expensive and noisy; calibrate it.

## 4 Judge design

- Use a second model to score with rubric.
- Ask for:
  - strengths
  - weaknesses
  - reasoning
  - score
- Reasoning first reduces “safe middle” scores.
- Example structure:
  - task
  - solution
  - output JSON with score + rationale

### Calibration matters

- Compare judge scores against human labels.
- Measure agreement.
- If agreement is low:
  - tighten rubric
  - add examples
  - re-measure
- A judge without calibration is just a noisy guess.

## 5 Coverage > perfection

- A larger eval set with some noise beats a tiny hand-picked set.
- Include edge cases and weird inputs.
- Generate more examples from a small labeled seed set, then spot-check.
- The goal is to catch regressions, not perfect grading.

## 6 Use evals to diagnose failures

- Formatting issue -> bad output schema / prompt instructions
- Factual failure -> retrieval or grounding problem
- Long-input failure -> context handling / truncation
- Per-case error analysis tells you what to fix next.

## 7 Core takeaway

- Evals turn intuition into a measurable score.
- Code checks are best for structure.
- Judges are best for open-ended quality.
- Calibrate the judge.
- Change one thing at a time.
- The eval loop is: define goal -> run -> diagnose -> fix -> re-run.

## 8 Tradeoff

### Good

- Makes correctness measurable
- Enables iterative improvement
- Creates evidence for deployment decisions

### Cost

- Requires case creation and judge calibration
- More upfront work before shipping

### When to skip judge

- If the output is a fixed-format artifact, a code check may be enough.
