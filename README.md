# agent-skills

Reusable skills for AI coding agents (Claude Code, Codex, and other harnesses that load `SKILL.md` files).

## Skills

| Skill | What it does |
|---|---|
| [autopilot-github-execution](skills/autopilot-github-execution/SKILL.md) | Implements a GitHub issue end to end without checking in. Stops with one question if the issue is unclear, otherwise runs isolate → design → spec review → plan → plan review → subagent implementation → branch review, and reports "ready for PR" without pushing. |
| [filing-follow-up-issues](skills/filing-follow-up-issues/SKILL.md) | Files GitHub issues (including follow-ups found mid-task) with the same label groups and title prefix as the repo's current issues, read from `gh issue list` and `gh label list`, and verifies the labels after filing. |

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

`autopilot-github-execution` orchestrates skills from [obra/superpowers](https://github.com/obra/superpowers): `using-git-worktrees`, `brainstorming`, `writing-plans`, `subagent-driven-development`, `test-driven-development`, `requesting-code-review`, and `verification-before-completion`. Install those first. It also expects a GitHub MCP server so the agent can read the issue body, labels, and comments. It requires `filing-follow-up-issues` (in this repo) for any issue it files during a run.

`filing-follow-up-issues` needs the [GitHub CLI](https://cli.github.com/) (`gh`), authenticated for the repo.

## Layout

```
skills/
  <skill-name>/
    SKILL.md
```

Each skill is self-contained in its own folder.

## License

[MIT](LICENSE)
