## Prompt: Longer ≠ Better — Revision Notes

- **Core idea:** Adding words often masks a missing structural constraint. Diagnose before you lengthen prompts.

- **Typical failure pattern:**
  - Repeated re-prompts grow verbose but still drift in format, case, or edge cases.
  - Verbose prompts can increase output length and latency without improving accuracy.

- **Minimal fix that usually works:**
  - Add an explicit output constraint or JSON schema.
  - Add 1–2 few-shot examples (include an ambiguous example).

- **Two common mistakes:**
  - _Diagnostic failure:_ misidentify problem and add description instead of a constraint.
  - _Engineering failure:_ verbosity causes long, unfocused outputs and latency regressions.

- **Practical rule:** If 3 re-prompts haven't fixed it, stop adding prose — diagnose and apply one structural fix.

- **Example (condensed):**
  - Problem: inconsistent labels and parser failures.
  - Fix: system instruction + output constraint (e.g., return only BILLING/TECHNICAL/ESCALATION) + few-shot examples.
  - Result: consistent, machine-parseable outputs and lower latency.

- **Quick checklist:**
  - Name the observed failure before editing.
  - Prefer schema or explicit constraint over long descriptions.
  - Use 1–2 targeted examples, including ambiguous cases.
  - Monitor output length and latency after changes.

---

Keep this as a short decision card when prompts start growing but results don't improve.
