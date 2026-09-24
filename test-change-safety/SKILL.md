---
name: test-change-safety
description: Decide how to handle a failing or existing test that someone proposes to edit, skip, delete, or weaken.
---

# Test Change Safety

Treat existing tests as evidence of intended behavior. A failing test is a reason to investigate, not by itself a reason to change the test.

## Before changing an existing test

1. Reproduce or inspect the failure and read the behavior the test protects.
2. Find the governing source of truth: the user's approved request, current product or technical documentation, public contracts, and applicable repository policy.
3. Classify the cause:
   - **Implementation regression:** fix the code and keep the test.
   - **Approved behavior change:** update the test and relevant contracts or docs together.
   - **Incorrect test:** correct it with an explanation of the expected behavior.
   - **Brittle test:** assert observable behavior while preserving meaningful coverage.
   - **Flaky or environmental test:** stabilize or isolate the cause; do not remove behavioral coverage just to silence it.
   - **Obsolete behavior:** remove the test only when the behavior is genuinely removed and its other references are updated.
4. If the implementation conflicts with the higher-priority source of truth, treat the implementation as wrong unless the user has authorized a behavior change.

Do not edit a test merely because production code changed, the assertion is inconvenient, or CI needs to pass.

## Higher-risk coverage

Identify which tests protect high-impact behavior in this project. Common examples include authentication, authorization, privacy, data retention, data integrity, public API behavior, payment or safety rules, and security boundaries. Apply the project's own change-approval rules to those tests.

If a test is removed, skipped, or weakened, preserve equivalent-or-stronger coverage where appropriate and state where it lives. Keep negative cases and important authorization or validation cases covered. A snapshot refresh should not hide a behavior change.

## Validation and reporting

Run the smallest relevant checks required by the task and repository policy. Broaden validation when the change is high-risk, cross-cutting, or explicitly requires it. Report the test change, its justification, the source of truth, replacement coverage, and checks run or not run.

If evidence is insufficient to classify a failure safely, keep the test and investigate the implementation or ask for the missing product decision.
