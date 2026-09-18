**Template That Couldn't Be Reused — Revision Notes**

- **Problem:** Hardcoded demo values made a template that ran but wasn't configurable or verifiable by others.

**Failure pattern**

- Values (repo paths, model name, thresholds, prompt fragments) were baked into code to meet a deadline.
- No parameters, no assumptions doc, and no bundled eval.
- Later teams couldn't reuse it and rewrote the template.

**Signs a template is not reusable**

- No clear parameters or config file.
- Missing README explaining assumptions and inputs.
- No eval or tests to validate behavior in a new environment.

**Fix checklist**

- Extract customer-specific values into a single config with documented defaults.
- Add README: purpose, inputs, environment, and failure modes.
- Provide a small eval suite or CI check with baseline scores.
- Add contribution/upgrade notes: where to change values and test steps.

**Quick tips**

- Package while the build is fresh — knowledge is cheap then.
- Make configuration obvious (one file, few keys).
- Use creds-by-reference and avoid embedded secrets.
- If genuinely one-off, note that explicitly in docs.

Keep this checklist with the template during packaging.
