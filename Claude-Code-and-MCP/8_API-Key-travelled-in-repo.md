## API Key in Repo — Revision Card

- The mistake is simple: an inline secret in .mcp.json got committed to git.
- A committed secret is not a temporary setup detail; it becomes part of repo history.

- What happened:
  - API key added directly to config for quick setup
  - config file committed to repo
  - key copied into local machines, teammate clones, and CI runner
  - service account had to be rotated after discovery

- Correct pattern:
  - store the secret in an environment variable
  - reference it in config
  - never commit the raw credential

- Example:
  - bad: Authorization: Bearer sk-abc123...
  - good: Authorization: Bearer ${WAREHOUSE_MCP_TOKEN}

- Why this matters:
  - overwriting the file later does not wipe the key from git history
  - any inline secret must be treated as compromised

- Prevention:
  - add a rule in CLAUDE.md: never write inline secrets to .mcp.json
  - add a PreToolUse hook to block suspicious patterns before they are written
  - use the hook as enforcement; use CLAUDE.md as intent

- Rule of thumb:
  - config files hold server addresses and references
  - secrets live in env vars or managed secret stores

Quick checklist

- Never commit raw API keys to .mcp.json
- Use env vars for all secrets
- Rotate any credential that was once committed
- Add a defensive hook for secret-writing patterns
- Treat config files as public metadata, not secret storage

### Q&A (flashcards)

1. **What was the main mistake?**  
   Committing a secret directly into .mcp.json.

2. **Why is that dangerous?**  
   The secret remains in git history even after the file is corrected.

3. **What is the correct pattern?**  
   Put the secret in an env var and reference it from config.

4. **What should you do if a key was already committed?**  
   Treat it as compromised and rotate it.

5. **Why use a hook as well as CLAUDE.md?**  
   The instruction is helpful, but the hook enforces it deterministically.

6. **Where should secrets live?**  
   In env vars or managed secret stores, not repo files.

7. **What belongs in .mcp.json?**  
   Server URL and references, not credentials.

8. **One-line rule?**  
   If it is a secret, it should not live in a committed config file.
