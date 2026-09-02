## Prompting Modes — Revision Notes

- **Three modes:**
  - **Zero-shot:** instruction only; no examples.
  - **One-shot:** add one example (input → desired output).
  - **Multi-shot / Few-shot:** include several examples to show exact answer shape.
  - Examples live in the prompt (not training data) to demonstrate format and edge cases.

- **Cost vs quality:**
  - Examples increase token cost and use context budget.
  - Use zero-shot for simple, obvious tasks; add 1–2 examples for structured or tricky outputs.
  - Prefer the minimal examples that reliably fix errors.

- **Interaction with model choice:**
  - Stronger models often succeed zero-shot where smaller models need examples.
  - Combine model tier and number of examples to meet evals cost-effectively.

- **Quick checklist:**
  - Start with zero-shot on a capable model; add examples if evals fail.
  - Prefer one or two targeted examples over long instructions.
  - Monitor token use and context limits when adding examples.

---

Use this as a quick reference when designing prompts and balancing cost vs reliability.
