# Token Saver — RTK Protocol

AI agent skill for filtering bash command output before it reaches the LLM context.
Saves **60-90%** tokens on git, test, install, lint, build, cloud, containers.
Default-on rule: try `rtk` for any long-output command.
Includes Tee Recovery Protocol for full error output on failures.

| | |
|---|---|
| **Repository** | [aetox-skills/token-saver](https://github.com/aetox-skills/token-saver) |
| **Status** | v0.1.2 |
| **Load with** | `skill("token-saver")` in any AI tool |
| **Platform** | Any AI coding tool (OpenCode, Claude Code, Codex, Cursor, Gemini CLI, ZCode) |

## Quick Reference

- **Default-on:** Any command with long output → prefix with `rtk`
- **Skip:** `echo`, `cp`, `mv`, `mkdir`, `which`, `git diff` (code review)
- **Bypass:** `rtk proxy <cmd>` for raw output
- **Tee Recovery:** On failure → read the tee file for full error output

## Links

- [Full Skill File](https://github.com/aetox-skills/token-saver/blob/main/SKILL.md)
- [RTK Official](https://github.com/rtk-ai/rtk) (67k⭐)
