---
name: issue-pr-workflow
description: GitHub issue/PR workflow rules for coding agents — issues as durable state, one PR per issue, native relations (sub-issues, blocking dependencies, labels) over prose, topic-branch discipline, merge on green.
---

## Issue and pull request workflow

A request from the user is durable state. Chat sessions are transient and will
be dropped, so the canonical record of what they asked for is a GitHub issue.
Open an issue for every user request before building, and let the issue body
carry the intent, constraints, and decisions made along the way.

A pull request has one of two purposes: a quick bug fix, or resolving an issue.
Do not split a single issue into multiple PRs because the implementation has
phases; use multiple commits on one branch instead. One PR corresponds to one
resolved issue or one discrete bug fix.

Structure between work items uses GitHub's native features rather than prose: a
request with separable parts decomposes into sub-issues under a parent issue,
each leaf issue resolved by its own PR; ordering goes in blocking/blocked-by
dependencies, and classification in labels, issue types, and milestones. Native
metadata is queryable and auditable — a markdown checklist or a "depends on #N"
line in the body is not. The issue body still carries intent, constraints, and
decisions; anything GitHub can express structurally is expressed structurally.

When the user updates a requirement or adds context, update the existing issue
rather than opening a new one. If the change is an addition, edit the issue body
or add a comment. If it corrects a prior misunderstanding, rewrite the issue
body so it reflects their actual intent. The issue and its linked PR together
must tell the full story of the work and the user's intent.

Do not open an issue for a bug that is already understood, freshly introduced,
and trivial to fix in the same pass. In that case open the PR directly, with a
clear title and body describing the cause and fix.

Work lands on a topic branch pushed with `git push -u origin <branch>`; never
push to protected or default branches directly. Open the PR against the
repository's integration branch (`gh pr create --base dev` in repositories that
maintain a `dev` integration branch, otherwise the default branch). A PR that
resolves an issue includes `Fixes #N` in the body. Merging is the user's
decision; unless they object in the conversation, merge the PR once every check
it can affect is green.

Never open an issue, discussion, or PR on a repository the user does not own,
and never comment on someone else's issue or PR, without their permission for
that specific filing. Anything sent upstream carries the user's name and must be
hand-verified by them first.
