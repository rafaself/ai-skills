# AI Skills

A small collection of reusable engineering workflows for Codex and other agents that read Agent Skills.

Each skill is an independent folder with a **SKILL.md** manifest. The top-level folders are the source copies in this repository. To make one discoverable as a repository-local Codex skill, copy its folder into the target repository's **.agents/skills/** directory.

## Skills

| Skill | Use it for |
| --- | --- |
| [Review Code Changes](review-code-changes/SKILL.md) | Findings-first review of a diff, commit, branch, or pull request. |
| [Defensive Security Review](defensive-security-review/SKILL.md) | Defensive review of security and privacy risks. |
| [Test Change Safety](test-change-safety/SKILL.md) | Deciding how to handle a failing or proposed-to-change existing test. |
| [API Contract Change Safety](api-contract-change-safety/SKILL.md) | Changes to observable API behavior and its schemas, clients, and documentation. |
| [Sequential Task Orchestrator](sequential-task-orchestrator/SKILL.md) | Coordinate an explicitly ordered batch through one sub-agent at a time. |

## Install with Codex recommendations

Ask Codex to recommend a skill for your task from this repository. For example:

```text
I need to review a pull request. Which skill from https://github.com/rafaself/ai-skills fits best?
```

After Codex recommends one, install it with the built-in `$skill-installer` skill and the GitHub URL for that skill's folder. For example:

```text
$skill-installer
Install the skill from https://github.com/rafaself/ai-skills/tree/main/review-code-changes
```

Codex installs it in your user skills directory (`$CODEX_HOME/skills`, or `~/.codex/skills` by default). It will be available on your next turn. For Codex's documented `$skill-installer` command form, see [OpenAI's Codex example](https://developers.openai.com/blog/designing-delightful-frontends-with-gpt-5-4).

## Adapt them to each project

These skills provide workflows, not universal project policy. Before using one in another repository, adapt its sources of truth, technical stack, threat model, approval boundaries, severity conventions, commands, and validation requirements to that project. Follow the target repository's AGENTS.md and other local guidance.

Do not assume any rule, architecture, or command from the skills' source project applies elsewhere. The skills do not grant permission to edit tests, access production systems, change contracts, or perform external actions. Resolve project-specific decisions from the destination project's current documentation and authorized requests.

## Codex format and discovery

OpenAI documents skills as folders with a SKILL.md containing a name, a trigger description, and workflow instructions; references, scripts, and assets are optional. Codex repository skills are commonly kept under .agents/skills/. This repository keeps the distributable folders at its root for easy browsing; copy only the skills a project needs into that project's .agents/skills/ directory.

Keep skill descriptions specific about when they apply. Keep repository-wide conventions in the destination project's AGENTS.md, and put reusable task workflows in skills.

See [OpenAI's Skills guide](https://developers.openai.com/plugins/concepts/skills) and [Codex skills in OSS maintenance](https://developers.openai.com/blog/skills-agents-sdk) for the format and repository-local discovery model.
