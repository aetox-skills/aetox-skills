# Aetox Skills

Aetox Skills is a public catalog of AI agent skills for software builders.

These skills help AI agents work with clearer discipline: inspect before
acting, preserve user intent, avoid duplicated documentation, mark uncertainty,
and leave useful context for future humans and AI agents.

This repository is the central index for the Aetox skill family. Each major
skill lives in its own repository.

Core search terms: AI agent skills, Codex skills, architecture mapping,
software architecture documentation, AI agent handoff, existing system mapping,
raw idea to architecture proposal, and documentation architecture.

## Current Skills

| Skill | Use when | Repository | Status |
| --- | --- | --- | --- |
| Senior Architect Agent | AI architecture skill for existing system mapping, software architecture documentation, boundaries, risks, Mermaid diagrams, and AI agent handoff. | [senior-architect-agent](https://github.com/aetox-skills/senior-architect-agent) | v1.1.0+ |
| Idea To Architecture Agent | Raw ideas, product concepts, feature requests, and business goals need reviewable architecture proposals. | [idea-to-architecture-agent](https://github.com/aetox-skills/idea-to-architecture-agent) | v0.1.0+ |
| DocStruct | Project documentation needs clear ownership, one source of truth, less duplication, and lower token cost. | [docstruct](https://github.com/aetox-skills/docstruct) | v0.2.0+ |
| Deep Study | ศึกษาอะไรก็ได้ (repo, concept, paper, framework, system) แล้วเขียนตำราให้เข้าใจจริง — Research Pipeline + Knowledge Density 5 ชั้น + Study Plan | [deep-study](https://github.com/aetox-skills/deep-study) | v0.1.0 |
| Token Saver | CLI proxy ที่กรอง output bash command ช่วยประหยัด tokens 55-90% สำหรับ git, test, install, find, docker | [token-saver](https://github.com/aetox-skills/token-saver) | v0.34.3 |

## Skill Routing

Use the smallest skill that fits the work.

- Use `senior-architect-agent` for existing codebases, system mapping,
  architecture documentation, system boundaries, risks, and AI handoff.
- Use `idea-to-architecture-agent` for pure raw ideas without an existing
  implementation.
- Use `docstruct` for documentation structure, documentation audits, source of
  truth cleanup, and token-efficient project docs.
- Use `token-saver` for RTK Protocol — always prefix noise-producing bash
  commands with `rtk` to save LLM tokens.

If a task mixes existing system evidence with a proposed future change, start
with `senior-architect-agent`.

If a task is only about keeping project documentation clear and non-duplicated,
use `docstruct`.

## Core Principles

- Practical over theoretical.
- Clear over clever.
- Small before large.
- Agent behavior over prompt decoration.
- Reusable skills over one-time instructions.
- Human-readable and agent-usable.
- Markdown as the durable source of truth.
- Explicit uncertainty instead of hidden assumptions.

## Cross-Agent Support

Each skill repository follows the **standard template** at
[aetox-skills/skill-template](https://github.com/aetox-skills/skill-template):

| File | Purpose |
|------|---------|
| `README.md` | Overview, use cases, quick reference |
| `SKILL.md` | Core agent instruction file — load with `skill("[name]")` |
| `INSTALL.md` | Cross-platform setup guide |
| `CHANGELOG.md` | Version history |
| `LICENSE` | Apache 2.0 |

To create a new skill, click **"Use this template"** on the
[skill-template](https://github.com/aetox-skills/skill-template) repo.

The goal is not to create a platform. The goal is to make each skill portable
across modern AI agent environments.

## Install

Install each skill from its own repository:

```txt
aetox-skills/senior-architect-agent
aetox-skills/idea-to-architecture-agent
aetox-skills/docstruct
```

See each repository's `INSTALL.md` for platform-specific guidance.

## Not A Bulk Prompt Collection

Aetox Skills is not a dump of random prompts.

Each skill should have:

- a clear purpose
- a specific usage context
- practical operating rules
- examples or templates when useful
- a reason to exist as a reusable agent behavior package

If a skill does not improve agent behavior, it does not belong here.

## License

MIT. See [LICENSE](LICENSE).
