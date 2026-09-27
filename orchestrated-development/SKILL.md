---
name: orchestrated-development
description: Orchestrate multi-delivery development by delegating implementation to subagents, integrating their commits, and arranging independent review. Use when the user requests delegation or a task benefits from staged implementation.
---

# Orchestrated Development

Use this workflow to keep the main agent focused on the user's intent, planning, integration, and final ownership while subagents handle bounded implementation work.

## Governing instructions

- Follow all applicable higher-priority instructions and repository guidance. Within those boundaries, treat the user's complete prompt as the governing task specification; this skill supplies defaults only where the prompt is silent.
- Carry the original user prompt, or a faithful brief preserving every relevant requirement, constraint, exception, and detail, into each subagent assignment. Add the assigned delivery, its acceptance criteria, and relevant repository instructions. A narrower subtask must not silently discard or contradict the user's requirements.
- If the prompt, repository instructions, or task details materially conflict or leave an important decision unresolved, have the main agent resolve it or ask the user before dependent work proceeds.
- Inspect applicable `AGENTS.md` and contribution guidance. Preserve unrelated user changes. A local commit does not authorize pushing, publishing, deployment, or other remote actions.

## Plan deliveries

- If the user supplied deliveries, check their order, dependencies, boundaries, and acceptance criteria. Preserve the requested breakdown unless a dependency or conflict requires adjustment.
- If no breakdown was supplied, have the main agent divide the work into the smallest useful, reviewable deliveries. Keep tightly coupled changes together and avoid splitting work just to create more agents.
- Delegate when the user requests it or when multiple meaningful deliveries benefit from independent implementation. For a trivial, tightly coupled task where delegation adds overhead, the main agent may work directly unless the user explicitly requested subagents.
- Identify the integration branch or checkout from the user's instructions and repository state. Do not switch branches or disturb pre-existing changes without reason.

## Implement serially by default

- Spawn one implementation subagent at a time and wait for its completion before starting the next. Default to model `gpt-6-luna` with reasoning effort `max`, unless the user specifies a different model or effort.
- Assign one delivery per worker. Tell the worker to follow the supplied user requirements and repository rules, stay within the delivery scope, make and commit its task changes, perform the requested or applicable validation, and report changed files, commit SHA, checks and results, and blockers.
- Do not ask a worker to commit unrelated changes. Do not let a worker push or perform external actions unless the user authorized those actions.
- After each worker completes, inspect its actual diff and commit, compare the result with the acceptance criteria, and resolve or report blockers before continuing. Do not rely only on the worker's summary.

## Optional parallel implementation

- The main agent may add one second implementation worker (two implementation workers total) only when the workstreams are independent, do not contend over shared files or mutable resources, and parallel execution is useful.
- Give the second worker a separate worktree and branch. If the available tools cannot provide an isolated worktree, keep implementation serial.
- Integrate both workers' commits into the chosen integration branch. Inspect the combined diff, resolve conflicts deliberately, and validate the integrated result. Do not assume separate work is correct merely because each worker committed successfully.
- Remove only worktrees and branches created for this run, and only after confirming their work is integrated and they contain no uncommitted or unmerged work. Leave pre-existing or unrelated worktrees and branches alone.

## Independent review and remediation

- After all implementation work is integrated, spawn a separate review subagent to inspect the final change against the original user prompt, acceptance criteria, and relevant repository guidance. Give it the base-to-integration diff and ask it to report actionable findings with evidence and severity. The reviewer should not modify files.
- If the review finds actionable issues, spawn a separate remediation subagent and give it the findings, original task requirements, and relevant repository instructions. Ask it to address the findings within scope, commit its changes, and report the commit and validation evidence.
- If the review finds no actionable issues, skip remediation.
- After remediation, the main agent inspects the fix and verifies that findings were addressed. If an issue remains after one focused remediation pass, report it and ask the user how to proceed instead of looping indefinitely.

## Close out

- The main agent owns the final result. Inspect the integrated diff, commits, review findings, remediation, and repository state. Run validation requested by the user or required by applicable project guidance; report what was and was not run accurately.
- Finish any eligible worktree and branch cleanup described above.
- Report the deliveries completed, relevant commit identifiers, review and remediation outcome, validation evidence, and any unresolved items.
