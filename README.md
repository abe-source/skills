<p align="center">
  <img src="assets/hero.svg" alt="skills" width="100%" />
</p>

<p align="center">
  <a href="https://github.com/abe-source/skills/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-facc15.svg" alt="MIT License"></a>
  <img src="https://img.shields.io/badge/SKILL.md-open%20standard-facc15.svg" alt="SKILL.md open standard">
</p>

Reusable AI-agent skills I've built and use day to day — packaged up and published here as they're generalized enough to be useful to anyone, not just tied to my own setup.

## What's a skill

A skill is a folder with a `SKILL.md` file: a description (so the agent knows when to use it) plus instructions for carrying out a specific task. `SKILL.md` is an open standard — the same skill folder works unmodified across [Claude Code](https://docs.claude.com/en/docs/claude-code/skills), Codex CLI, Gemini CLI, Cursor, GitHub Copilot, and other compatible tools.

## Skills

| Skill | What it does |
|---|---|
| [`upwork-portfolio-item`](upwork-portfolio-item) | Produces the cover image, demo screenshot, and title/description/tags copy for adding a shipped project to your Upwork portfolio |

## Installation

Drop a skill's folder into your tool's skills directory:

```bash
git clone https://github.com/abe-source/skills.git
cp -r skills/<skill-name> ~/.claude/skills/   # or ~/.codex/skills/, ~/.gemini/skills/, etc.
```

## License

MIT
