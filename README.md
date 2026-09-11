# gh-workflow-rules

Instruction packages that install GitHub issue/PR workflow rules into a coding
agent's always-on rule files (`AGENTS.md` / `CLAUDE.md`) — instead of skills
that reload after every compaction and can silently conflict with existing
instructions.

## Packages

- `issue-pr-workflow/` — issues as durable state, one PR per issue, GitHub
  native relations (sub-issues, blocking/blocked-by, labels, milestones) over
  prose, topic-branch discipline, merge on green, consent before filing
  anything upstream.

## Install

With [agent-md](https://github.com/lexoliu/agent-md):

```sh
npx agent-md install gh:lexoliu/gh-workflow-rules
# or
bunx agent-md install gh:lexoliu/gh-workflow-rules
```

You pick which agent performs the merge (Claude Code or Codex) and which files
to install into; the agent merges into a staging copy — asking you when your
existing rules conflict — and `agent-md` shows you the diff for approval before
anything is written.
