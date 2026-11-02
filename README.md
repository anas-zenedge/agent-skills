# agent-skills

Reusable skills for AI coding agents (Claude Code, Kilo Code, Codex, and other harnesses that load `SKILL.md` files).

## Skills

| Skill | What it does |
|---|---|
| [autopilot-github-execution](skills/autopilot-github-execution/SKILL.md) | Implements a GitHub issue end to end without checking in. Stops with one question if the issue is unclear, otherwise runs isolate → design → spec review → plan → plan review → subagent implementation → branch review, and reports "ready for PR" without pushing. |

## Install

With the [`skills`](https://github.com/vercel-labs/skills) CLI:

```sh
# all skills
npx skills add anas-zenedge/agent-skills

# one skill
npx skills add anas-zenedge/agent-skills --skill autopilot-github-execution
```

Or copy a skill folder by hand:

```sh
git clone https://github.com/anas-zenedge/agent-skills
cp -r agent-skills/skills/autopilot-github-execution ~/.claude/skills/        # Claude Code, user level
cp -r agent-skills/skills/autopilot-github-execution <repo>/.claude/skills/   # Claude Code, project level
```

## Dependencies

`autopilot-github-execution` orchestrates skills from [obra/superpowers](https://github.com/obra/superpowers): `using-git-worktrees`, `brainstorming`, `writing-plans`, `subagent-driven-development`, `test-driven-development`, `requesting-code-review`, and `verification-before-completion`. Install those first. It also expects a GitHub MCP server so the agent can read the issue body, labels, and comments.

## Layout

```
skills/
  <skill-name>/
    SKILL.md
```

Each skill is self-contained in its own folder.

## License

[MIT](LICENSE)
