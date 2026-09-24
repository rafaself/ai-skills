---
name: release-pull-request
description: Prepare concise pull request text or open a pull request from the current branch to a requested base branch, following repository guidance and templates.
---

# Release Pull Request

Prepare a clear, concise pull request title and summary from the changes that will appear in the PR. Use this skill when the user asks to prepare, open, or update a pull request.

## Workflow

1. Read applicable repository instructions and look for a pull request template or documented contribution conventions.
2. Identify the head branch and requested base branch. If the base is omitted, use it only when the repository's PR settings or conversation make it unambiguous; otherwise ask.
3. Inspect the committed base-to-head diff and relevant context. Summarize the change's purpose and user-visible effect, not a file-by-file inventory or commit list. Exclude uncommitted work unless the user asks to include it.
4. Draft a short title and summary. Prefer one sentence; use up to three brief bullets only when they make distinct changes easier to understand. Follow a repository template when present, and fill other required fields only with facts supported by the diff or known validation results.
5. If the user asked only for PR text, return the draft without changing GitHub state. If the user asked to open or update a PR, use the configured GitHub CLI or integration and report the resulting URL. Before updating, verify the PR matches the intended head and base; ask only if the match is ambiguous.

## Boundaries

- Do not claim tests, checks, or deployments passed unless their results are known. Keep verification details out of the summary unless the template requires them.
- Do not commit, amend, stage, push, or change code as part of preparing PR text. If the branch is not available on the remote, explain what is missing and ask before pushing.
- Do not create a duplicate PR when one already exists for the same head and base; offer its URL and update it only when requested.
- Keep the summary focused on what changed and why it matters. Avoid review findings, speculative benefits, and generic statements such as “various improvements.”
