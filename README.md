# claude-plugins

Claude Code plugins marketplace for Diversio.

## Overview

This repository is a Claude Code marketplace that hosts reusable plugins (primarily Skills) maintained by the Diversio team.

## Repository Structure

```
claude-plugins/
├── .claude-plugin/
│   └── marketplace.json               # Marketplace definition
├── plugins/
│   ├── monty-code-review/             # Monty backend code review plugin
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json            # Plugin manifest
│   │   └── skills/
│   │       └── monty-code-review/
│   │           └── SKILL.md           # Skill definition
│   ├── backend-pr-workflow/           # Backend PR workflow plugin
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   └── skills/
│   │       └── backend-pr-workflow/
│   │           └── SKILL.md
│   └── code-review-digest-writer/     # Code review digest generator
│       ├── .claude-plugin/
│       │   └── plugin.json
│       └── skills/
│           └── code-review-digest-writer/
│               └── SKILL.md
├── README.md
└── LICENSE
```

## Available Plugins

| Plugin | Description |
|--------|-------------|
| `monty-code-review` | Hyper-pedantic Django4Lyfe backend code review Skill |
| `backend-pr-workflow` | Backend PR workflow Skill that enforces ClickUp-linked branch/PR naming, safe migrations, and downtime-safe schema changes |
| `code-review-digest-writer` | Weekly code-review digest writer Skill (repo-agnostic) |

## Installation

1. Add the marketplace to Claude Code:

   ```bash
   /plugin marketplace add DiversioTeam/claude-plugins
   ```

2. Install a plugin from the marketplace:

   ```bash
   # Monty backend code review
   /plugin install monty-code-review@diversiotech

   # Backend PR workflow (ClickUp + migrations/downtime)
   /plugin install backend-pr-workflow@diversiotech

   # Code review digest writer
   /plugin install code-review-digest-writer@diversiotech
   ```

## Documentation

- [Claude Code Plugins](https://code.claude.com/docs/en/plugins)
- [Plugin Marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Agent Skills](https://code.claude.com/docs/en/skills)

## License

MIT License - see [LICENSE](LICENSE) for details.
