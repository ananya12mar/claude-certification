## OAuth Failed in Prod — Revision Card

- A staging OAuth flow working does not guarantee production works.
- Redirect URIs are host- and environment-specific.

- Root cause:
  - staging host was registered
  - production host was not
  - sign-in failed at redirect validation

- Key rule:
  - add the production redirect URI to the OAuth app registration before deployment
  - verify whether staging and prod need separate app registrations

- Enterprise pattern:
  - separate OAuth apps per environment is common in regulated orgs
  - same app across envs is often a security and compliance issue

- Deployment checklist:
  - register correct redirect URIs for each host
  - confirm environment separation policy
  - test the real production sign-in path before relying on staging

Quick checklist

- Register redirect URI for prod host
- Check whether staging and prod must be separate apps
- Include OAuth registration in deployment checklist
- Test production auth, not just staging

### Q&A (flashcards)

1. **Why did staging pass but prod fail?**  
   The OAuth app was registered for staging, not production.

2. **What are redirect URIs tied to?**  
   Host and environment.

3. **What is the usual fix?**  
   Add the production host’s redirect URI to the OAuth registration.

4. **What should enterprise teams check?**  
   Whether staging and production need separate OAuth app registrations.

5. **What is the real lesson?**  
   OAuth configuration is environment-specific, not just code-specific.

6. **What should be added to deployment checks?**  
   OAuth registration and redirect validation.

7. **How should you test?**  
   Run the real production sign-in path, not only staging.

8. **One-line rule?**  
   OAuth is configured per host and per environment; staging success does not authorize production.
