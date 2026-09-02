## Models & Reasoning — Revision Notes

- **Model tiers (practical):**
  - **Fable:** highest capability — best for hardest reasoning/coding/agentic work.
  - **Opus:** above Sonnet for demanding tasks.
  - **Sonnet:** balanced default for most production use.
  - **Haiku:** fastest and cheapest for tasks that fit its ability.
  - **Rule of thumb:** start with Sonnet; move up only after evals show quality gaps; move down only if quality drop is acceptable.
  - **Action:** confirm current lineup/identifiers in platform docs at build time.

- **Reasoning modes (per request):**
  - Reasoning (adaptive thinking) is configured per call and is separate from model choice.
  - Control thinking depth with an `effort` setting; `budget_tokens` is deprecated on newer models.
  - Newer models may omit internal thinking from visible responses by default — request summarized display if you need it.
  - Use reasoning for multi-step problems; avoid it for simple lookups/classification.

- **How they combine:**
  - They compose: model selects capability; reasoning controls how much internal deliberation occurs.
  - Capable model + reasoning off = fast; smaller model + reasoning on = slower, more token use.
  - For hardest tasks: pair a higher-tier model with higher `effort`.

- **Quick checklist:**
  - Verify model IDs and defaults in platform docs.
  - Start with Sonnet; eval before switching tiers.
  - Prefer `effort` tuning; avoid deprecated controls.
  - If you need to show thinking, request summarized display.

---

Use this as a compact reference when choosing models and configuring reasoning for calls.
