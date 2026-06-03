# Aetox Skills

Practical AI agent skills for building, documenting, and automating software systems.

Aetox Skills is a growing collection of open-source skills created under the Aetox project.
Each skill is designed to help AI agents work with better structure, less noise, and clearer judgment.

This repository is the central catalog for Aetox Skills.

It does not contain the full content of every skill.
Each major skill lives in its own repository.

---

## What Is Aetox?

Aetox is an independent AI systems project by Mike.

It focuses on building useful tools, workflows, and reusable agent skills for software builders who work with AI-assisted development.

Aetox is not trying to be a large framework.

The goal is simple:

> Build practical skills that help humans and AI agents work together with more structure, clarity, and execution power.

---

## Why Aetox Skills Exists

AI agents can write code, create documents, plan tasks, and assist with software systems.

But without clear working rules, they often:

* create too many files
* duplicate information
* over-document simple tasks
* mix unrelated responsibilities
* invent missing details
* waste context and tokens
* produce outputs that look complete but are hard to maintain

Aetox Skills exists to give agents reusable behavior patterns.

Each skill should help an agent make better decisions, not just produce more text.

---

## Core Principles

Aetox Skills follows these principles:

* Practical over theoretical
* Clear over clever
* Small before large
* Structure without overbuilding
* Agent behavior over prompt decoration
* Reusable skills over one-time instructions
* Human-readable and agent-usable
* Built by one builder, designed for many agents

---

## Current Skills

| Skill     | Description                                                                                       | Status | Repository                                             |
| --------- | ------------------------------------------------------------------------------------------------- | ------ | ------------------------------------------------------ |
| DocStruct | Documentation architecture skill for clear, non-duplicated, token-efficient project documentation | v0.1.x | [docstruct](https://github.com/aetox-skills/docstruct) |

---

## Skill Categories

Aetox Skills may grow into several categories:

### Documentation Skills

Skills for creating, organizing, auditing, and maintaining project documentation.

Current skill:

* DocStruct

### Code Structure Skills

Skills for helping agents understand project architecture, file boundaries, naming, and implementation structure.

Planned skills:

* CodeStruct

### Prompt and Agent Instruction Skills

Skills for writing better agent instructions, task prompts, and reusable command patterns.

Planned skills:

* PromptStruct

### Task and Workflow Skills

Skills for breaking down work, creating handoffs, planning execution, and tracking progress.

Planned skills:

* TaskStruct
* Agent Handoff

---

## How Skills Are Organized

Each major skill should have its own repository.

Example:

```txt
aetox-skills/
|-- aetox-skills     # central catalog
|-- docstruct        # documentation architecture skill
|-- codestruct       # future code structure skill
|-- promptstruct     # future prompt skill
`-- taskstruct       # future task workflow skill
```

This keeps each skill focused and easy to use.

The central catalog links to each skill, explains the overall direction, and tracks the ecosystem.

---

## How To Use

Choose the skill that matches the work you want an AI agent to perform.

For example:

Use **DocStruct** when you want an agent to:

* initialize project documentation
* audit existing docs
* reduce duplicated Markdown
* separate frontend, backend, API, and database docs
* keep documentation concise and useful
* avoid token-wasting documentation habits

Go to the skill repository and follow its README.

---

## Current Roadmap

### v0.1

* Publish the first usable skill: DocStruct
* Create the Aetox Skills catalog
* Establish naming, structure, and basic principles

### v0.2

* Improve DocStruct installation and adapters
* Add agent-specific usage examples
* Add more practical prompts

### v0.3

* Introduce the next skill candidate
* Add contribution rules
* Add shared community health files

---

## Not A Bulk Prompt Collection

Aetox Skills is not a dump of random AI prompts.

Each skill should have:

* a clear purpose
* a specific usage context
* practical rules
* agent-facing instructions
* examples or templates when useful
* a reason to exist as a reusable skill

If a skill does not improve agent behavior, it does not belong here.

---

## Contributing

This project is still early.

For now, contributions should focus on:

* improving clarity
* reducing unnecessary complexity
* making skills easier to use
* adding practical examples
* finding duplicated or vague instructions

Avoid adding large frameworks, abstract theory, or generic prompt collections.

---

## License

MIT

Copyright (c) Mike and Aetox Skills contributors.
