---
name: filing-follow-up-issues
description: Use when creating a GitHub issue, including follow-up issues found while implementing, reviewing or planning another issue, and before running gh issue create or a GitHub MCP issue-create tool.
---

# Filing Follow-up Issues

## Overview

A new issue carries the same label groups and title shape as the repo's current issues. An issue without them misses triage, boards and automations that key on labels, and the branch it should target.

## Read the convention

Before the first issue in a session, run:

```
gh issue list --state all --limit 15 --json number,title,labels
gh label list
```

From the output, write down:
- each label group the recent issues carry, for example type (`bug`, `enhancement`), target branch (`target: develop`), priority (`priority: medium`)
- the title shape, for example `[Medium] Area: symptom`

## The command

Every issue is created with this shape. Each slot is REQUIRED; a plan or user that gives only a title does not remove a slot.

```
gh issue create --repo <owner>/<repo> \
  --title "<title in the recent issues' shape, including any prefix>" \
  --label "<label from group 1>" --label "<label from group 2>" ... \
  --body-file <file>
```

With a GitHub MCP issue-create tool, pass the same title and labels.

| Slot | How to choose |
|---|---|
| One label per group | Pick by the label's description in `gh label list` (priority labels usually define their levels there) |
| Target branch label | The repo's default target; another branch only when the user asks |
| Title prefix | Matches the chosen label where recent titles do (for example `[Medium]` with `priority: medium`) |

Add these when their condition holds:

| Condition | Add |
|---|---|
| The body says a product decision is needed before implementation | The repo's needs-clarification label, if one exists |
| Recent issues of the same kind carry another label (an epic or programme label) | That label |

Never create a new label. Do not set a milestone or project unless the user asks.

## After filing

Run `gh issue view <n> --json title,labels`. Report each issue as: number, title, labels, and one line on why that priority.

## Red flags

- `gh issue create` with only `--title` and `--body-file`
- "The plan gave me the title", so the title lacks the repo's prefix
- "Triage will label it later": you are triage
