---
name: review-code-changes
description: Review a diff, commit, branch, or pull request for concrete correctness, security, contract, and regression issues.
---

# Review Code Changes

Review the behavior introduced or exposed by the requested change. Do not modify files unless the user asks for implementation.

## Resolve the review scope

Use the scope the user named. For a PR, inspect its base-to-head diff; for a commit, compare it to its parent; for a range or two refs, inspect that range; for working-tree or staged changes, inspect only that requested scope. If the base is unclear and there is no safe default, ask one concise question. State the exact scope and refs in the report.

## Review method

1. Inspect the diff before forming findings. Read surrounding implementation and relevant tests, contracts, documentation, and configuration as needed to understand behavior.
2. Trace affected flows across boundaries that matter to the change, such as API contracts, authorization, persistence, clients, UI state, caching, logging, and public/private routes.
3. Check realistic failure cases. Do not infer correctness from names, comments, or intent alone.
4. Review changed existing tests carefully: look for removed assertions, weaker matchers, skipped coverage, deleted negative cases, or snapshots that conceal behavior changes.
5. Consider validation evidence and identify important gaps; do not claim checks passed unless their results were inspected.

## Findings

Report only concrete, defensible issues introduced or exposed by the reviewed change. Prioritize data loss or incorrect data, security and privacy regressions, user-visible failures, contract drift, concurrency or cache errors, performance problems with concrete impact, and missing tests for risky behavior.

Each finding should include:

- Severity appropriate to the project, with a clear impact.
- File and line reference.
- The broken behavior and a concrete scenario.
- A practical fix.
- Whether relevant coverage exists.

Start with findings. If there are none, say so and mention material residual risks or validation gaps. Include open questions only when needed, then finish with the reviewed scope and verification details.

Do not report style preferences as bugs. Do not modify code, tests, or configuration during a review unless the user changes the request to implementation.
