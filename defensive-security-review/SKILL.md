---
name: defensive-security-review
description: Use for focused security or privacy reviews, especially changes that cross trust boundaries or handle sensitive data.
---

# Defensive Security Review

Perform a defensive review. Focus on whether the change preserves the system's security and privacy guarantees; do not provide exploit instructions or perform intrusive actions.

## Scope and context

Identify the reviewed scope, changed runtime surfaces, trust boundaries, sensitive data, and relevant project security documentation. Read the repository's local instructions and threat model when available. Tailor the review to the application's architecture and deployment environment.

For a change review, stay anchored to changed surfaces and expand only to verify relevant flows. Do not imply full-system coverage unless that scope was reviewed.

## Review areas

Check the areas relevant to the change:

- Authentication, authorization, ownership checks, and intentional public access.
- Input validation, output encoding, error behavior, and abuse controls.
- Secret and token handling, configuration, and exposure through source, tests, or logs.
- Personal or sensitive data in storage, browser state, telemetry, logs, and audit events.
- Network and file access boundaries, including redirects and user-controlled destinations.
- Dependencies, runtime permissions, deployment configuration, and unintended exposure.
- Consistency with the project's privacy, retention, incident-response, and security policies.

Do not assume every area applies. Follow the project's approved tools, review boundaries, and authorization rules; do not probe live systems or make external changes unless explicitly authorized.

## Report

Order findings by severity. For each, identify the affected file or configuration, the threatened asset or invariant, a realistic impact scenario, and the smallest effective mitigation. Distinguish verified issues from uncertainty and note important coverage or evidence gaps.

Keep the review defensive and actionable. Do not turn speculative possibilities into findings.
