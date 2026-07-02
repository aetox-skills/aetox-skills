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

## Catalog

### Agent Skills

| Skill | What it does | When to use | Repo |
|:--|:--|:--|:--|
| **Senior Architect Agent** | Maps existing systems — discovers structure, boundaries, risks, and produces architecture documentation + Mermaid diagrams. Generates handoff notes for the next AI agent. | You need to understand a codebase you didn't write, document technical debt, or hand off context to another agent. | [senior-architect-agent](https://github.com/aetox-skills/senior-architect-agent) |
| **Idea To Architecture Agent** | Takes raw ideas, product concepts, or feature requests and produces reviewable architecture proposals with assumptions, risks, and tradeoffs. | You have a vague idea or a feature request and need a structured architecture document before writing code. | [idea-to-architecture-agent](https://github.com/aetox-skills/idea-to-architecture-agent) |
| **DocStruct** | Audits and restructures project docs for clarity, single source of truth, less duplication, and lower token cost. Produces ownership maps. | Your project docs are scattered, duplicated, or bloated — you need a token-efficient documentation system. | [docstruct](https://github.com/aetox-skills/docstruct) |
| **Deep Study** | Research pipeline that studies any topic (repo, concept, paper, framework, system) and produces a textbook-quality explanation in 5 layers of Knowledge Density. | You need to truly understand something — not just skim. Produces a readable reference for humans and AI. | [deep-study](https://github.com/aetox-skills/deep-study) |

### Token Economy

| Tool | What it does | When to use | Repo |
|:--|:--|:--|:--|
| **Token Saver** | CLI proxy (RTK) that intercepts bash commands and filters their output before the LLM sees it. Compresses git logs, test results, install logs, and find output. **Saves 55–90%** of tool output tokens per command. | Any AI coding tool that runs bash commands. Run `rtk git log`, `rtk cargo test`, `rtk npm install` — the proxy strips noise and keeps what matters. | [token-saver](https://github.com/aetox-skills/token-saver) |
| **Token Calc** | Measures your system prompt size, estimates per-call costs, projects token usage across 1–500 calls with compounding cache hit rates. Multi-platform (OpenCode, ZCode, Claude Code). | You want to know how much each session costs before the bill arrives. Run the script, read the projection. | [token-calc](https://github.com/aetox-skills/token-calc) |

### OpenCode Plugins

| Plugin | What it does | When to use | Repo |
|:--|:--|:--|:--|
| **History Trimmer** | OpenCode plugin that trims conversation history intelligently — keeps up to 5 user questions (prioritized), hard cap at 10 total. Assistant responses and tool results get trimmed before user messages. **Saves ~97% vs uncapped history.** | You use OpenCode for long sessions and want history bloat gone without losing what matters. Default: 5 user messages + 10 total cap. | [history-trimmer](https://github.com/aetox-skills/history-trimmer) |

## Architecture

How all the pieces fit together — from your input to the API call:

```
┌─────────────────────────────────────────────────────┐
│                   Your Input                        │
└─────────────────────┬───────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────┐
│  ① Plugin: history-trimmer                       │
│     hook: experimental.chat.messages.transform      │
│                                                     │
│     • system messages → เก็บ ALL                    │
│     • user messages → เก็บ 5 ล่าสุด                 │
│     • assistant/tool → เก็บเท่าที่ total ≤ 10       │
│     • tool results โดนตัดก่อน user เสมอ             │
└─────────────────────┬───────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────┐
│  ② System Prompt Assembly                          │
│                                                     │
│     instructions (3 files) → ~3.2K tok              │
│     agent identity          → ~2K tok               │
│     available skills (7)    → ~0.3K tok             │
│     MCP tool defs (4)       → ~5-10K tok            │
│     built-in tool defs      → ~4K tok               │
│     history (capped)        → ~2-3K tok             │
└─────────────────────┬───────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────┐
│  ③ Plugin: RTK (token-saver)                      │
│     hook: tool.execute.before                       │
│                                                     │
│     rewrite bash → rtk bash → output บีบ 55-90%    │
│     (git, test, install, find, curl, tsc...)        │
└─────────────────────┬───────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────┐
│  ④ API (DeepSeek V4 Flash)                        │
│                                                     │
│     input: ~18-22K tok/system + history (~3K) + user│
│     cache hit rate: ~77%                            │
│     processed (pay): ~5K miss + ~2K output = ~7K    │
│     cost: ~$0.07 / 20 calls                         │
└─────────────────────────────────────────────────────┘
```

### Optimization Summary

| Layer | Before | After | Tool |
|:--|:--:|:--:|:--|
| Instructions | ~14K tok | ~3.2K tok | manual trim |
| AGENTS.md | ~3K | 0 | removed |
| MCP servers | 8 | 4 | commented out |
| Skills in path | 41 | 4 | moved to library |
| **History** | **~100K+** | **~5K** | **history-trimmer** |
| Bash output | raw | compressed | **token-saver (RTK)** |

**Result:** ~85% reduction. From ~$0.46/20 calls to ~$0.07/20 calls.

## Token Cost Per Call (approximate)

This table shows what each layer contributes to a single API call:

| Layer | Tokens | Optimized? |
|:--|:--:|:--:|
| OpenCode built-in (tool defs, system) | ~4K | ❌ built-in |
| Instructions (CONTEXT.md, PROFILE.md, index.md) | ~3.2K | ✅ trimmed |
| Available skills (7 × name + description) | ~0.3K | ⚠️ minor |
| MCP tool definitions (4 servers) | ~5–10K | ⚠️ comment out when idle |
| Agent identity (steward prompt) | ~2K | ✅ AGENTS.md empty |
| History (5 user + 10 total, role-aware) | ~4–5K | ✅ history-trimmer |
| **Total system prompt** | **~15–22K** | **~60–70% reduction** |

## Routing

Use the smallest tool that fits the work.

| Situation | Use |
|:--|:--|
| Need to map existing code, document architecture, or hand off to another agent | `senior-architect-agent` |
| Have a raw idea or feature request, need an architecture proposal | `idea-to-architecture-agent` |
| Project docs are messy, duplicated, or expensive in tokens | `docstruct` |
| Need to truly study a topic and produce reference material | `deep-study` |
| Running noise-producing bash commands (git, test, install) | `token-saver` — prefix with `rtk` |
| Want to measure and project token costs before a long session | `token-calc` |
| Long OpenCode session with growing history | `history-trimmer` — install once |

## Core Principles

- Practical over theoretical.
- Clear over clever.
- Small before large.
- Agent behavior over prompt decoration.
- Reusable skills over one-time instructions.
- Human-readable and agent-usable.
- Markdown as the durable source of truth.
- Explicit uncertainty instead of hidden assumptions.

## Standard Template

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

### Skills
Install each skill from its own repository:

```txt
aetox-skills/senior-architect-agent
aetox-skills/idea-to-architecture-agent
aetox-skills/docstruct
```

See each repository's `INSTALL.md` for platform-specific guidance.

### Plugins
Copy to `~/.config/opencode/plugins/` and restart OpenCode.

## License

MIT. See [LICENSE](LICENSE).
