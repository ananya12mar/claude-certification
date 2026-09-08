## Plugin Breaks in Prod — Revision Card

- Install success does not mean execution success.
- A plugin can install everywhere and still fail on every machine except the author’s own.

- Root cause:
  - absolute local paths were baked into a skill
  - an environment variable dependency was undocumented

- Example:
  - /Users/alexmorgan/projects/deploy-utils/validate.sh
  - works on author machine
  - fails for everyone else

- Why it breaks:
  - the plugin treated one machine as the shared environment
  - hidden dependencies are not visible in the package until runtime

- What to do instead:
  - use relative paths from project root or plugin root
  - prefer $CLAUDE_PROJECT_DIR for project files
  - prefer ${CLAUDE_PLUGIN_ROOT} for bundled plugin assets
  - document required env vars and validate them at install time
  - bundle required scripts/config with the plugin or store them in a shared project path

- Rule of thumb:
  - make the plugin portable before distribution
  - test on a clean machine before shipping

Quick checklist

- Remove hard-coded absolute paths
- Use project/plugin root variables
- Document required env vars
- Validate missing env vars early
- Test install on a clean machine

### Q&A (flashcards)

1. **Why can a plugin install but still fail?**  
   Installation and execution happen on different machines and resolve paths differently.

2. **What is the biggest error pattern?**  
   Hard-coded absolute file paths from the author’s machine.

3. **What is the safer path strategy?**  
   Use project-relative or plugin-root-aware variables.

4. **What should you do with required env vars?**  
   Document them and validate them during setup or install.

5. **Why are hidden env dependencies dangerous?**  
   The plugin appears to work until the step that needs the variable runs.

6. **What should you test before distribution?**  
   A clean-machine install and run.

7. **What should be bundled?**  
   Any scripts, config, or assets the plugin depends on.

8. **One-line rule?**  
   A plugin is only portable if it resolves paths and dependencies from the environment it is actually running in, not the author’s machine.
