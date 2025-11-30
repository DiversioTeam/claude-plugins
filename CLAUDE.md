@AGENTS.md

---

## Requirements & Commands

- Dependencies:
  - Claude Code installed locally.
  - This repo (`claude-plugins`) cloned on your machine.

- Add this marketplace to Claude Code (once this repo is hosted at GitHub):

  ```bash
  /plugin marketplace add DiversioTeam/claude-plugins
  ```

- Install the `monty-code-review` plugin from this marketplace:

  ```bash
  /plugin install monty-code-review@diversiotech
  ```

Once installed, the `monty-code-review` Skill will be available to Claude Code in
other projects and can be invoked for backend code review work.
