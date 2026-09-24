---
name: api-contract-change-safety
description: Change externally observable API behavior while keeping schemas, clients, and documentation aligned.
---

# API Contract Change Safety

Use this skill when a change can affect what an API consumer sends, receives, or is allowed to do. Do not use it for internal refactors with no observable contract change.

## Workflow

1. Describe the contract delta before editing: request or response shape, validation, status or error behavior, authentication or authorization, pagination, idempotency, or persistence-backed behavior.
2. Identify affected producers and consumers: server implementation, shared schemas, generated specifications, SDKs or clients, integrations, tests, and current documentation.
3. Check the project's compatibility and versioning rules. Identify consumers or deployments that may still depend on the old contract; do not assume a breaking change is safe.
4. Update affected implementation, schemas, generated artifacts, tests, and documentation together. Preserve existing conventions unless the authorized change explicitly changes them.
5. For a public error or domain-flow change, trace it through server mapping, published contract, and consumer handling.
6. Use the repository's focused validation commands and report any required checks that could not run.

## Safety

Follow the project's source of truth and migration process. Do not silently alter authentication, authorization, persistence, privacy, or error semantics. If a material rollout or compatibility decision is unclear, continue read-only investigation and request the necessary product or operator decision before making the consequential change.
