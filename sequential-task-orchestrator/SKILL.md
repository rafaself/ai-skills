---
name: sequential-task-orchestrator
description: Use only for explicitly requested sequential orchestration; delegate one ordered item at a time to a sub-agent while the parent tracks and reports instead of implementing. Not for parallel delegation.
---

# Sequential Task Orchestrator

Use this workflow only when the user asks you to coordinate an ordered batch and assigns you the orchestration role. Keep the parent task focused on delegation, waiting, tracking outcomes, and reporting; workers own the delegated work.

## Prepare the sequence

1. Resolve the exact ordered list from the request. Expand stated ranges inclusively, preserve the user's order, and use the actual final item when defining completion. Ask only if an identifier, boundary, or ordering is ambiguous.
2. Build a focused prompt for each item. Include its identifier and task-specific work, then carry forward shared constraints that apply to every item. Preserve repository guidance and explicit decisions about branches, validation, commits, pushes, pull requests, issue closure, tools, and when to stop for user input.
3. Do not invent additional work or permissions. The skill itself does not authorize consequential actions such as pushing changes, closing issues, merging, deploying, or contacting people; those actions must be authorized by the user's current request and remain within its scope.

## Run one item at a time

1. Start exactly one sub-agent for the next item, using the available delegation tool. Never have overlapping implementation workers in this sequential workflow.
2. Wait for that worker to finish before starting the next item. Prefer a blocking wait over frequent short polling. While it is running, do not duplicate its work, independently inspect its implementation, or supervise it unless the user changes the role or the worker needs a decision.
3. After a successful completion, record the worker's outcome and give a concise progress update before starting the next item.
4. If a worker encounters a clearly recoverable technical failure, allow a bounded, targeted recovery. Do not repeat an unchanged failed attempt or start overlapping work. If the work remains incomplete, stop the sequence unless the user explicitly directed you to continue past failures.
5. If a worker reports a blocker requiring user input, stop before dispatching later items and present the blocker. Do not silently skip, reorder, or mark an incomplete item successful.

If delegation or a reliable wait mechanism is unavailable, explain that this orchestration mode cannot run in the current environment; do not pretend the sequence completed.

## Report the result

After all items finish, summarize each completed item and any reported commit, validation, or external action. List blocked, failed, or unattempted items separately. Attribute results to the worker reports unless you independently verified them; do not claim checks or side effects succeeded without evidence. Keep the summary tied to the resolved sequence and its actual final item.
