# Token Saver — RTK Protocol

AI agent skill for filtering bash command output before it reaches the LLM context.
Saves **55-90%** tokens on git, test, install, find, docker, curl, json, and tsc.
Includes Tee Recovery Protocol for full error output on failures.

| | |
|---|---|
| **Repository** | [aetox-skills/token-saver](https://github.com/aetox-skills/token-saver) |
| **Status** | v0.34.3 |
| **Use when** | Running any bash command that produces long output |
| **Platform** | Any AI coding tool (OpenCode, Claude Code, Codex, Cursor, Gemini CLI) |

## Quick Reference

- **Always use `rtk` prefix:** `git`, `pytest`, `cargo test`, `npm/pip install`, `find`, `docker`, `curl`, `json`, `tsc`
- **Skip rtk:** `echo`, `cp`, `mv`, `mkdir`, `which`, `Test-Path`, `git diff` (code review)
- **Bypass:** `rtk proxy <cmd>` for raw output
- **Tee Recovery:** When command fails → read the tee file for full error output

## Links

- [Full Skill File](https://github.com/aetox-skills/token-saver/blob/main/SKILL.md)
- [RTK Official](https://github.com/rtk-ai/rtk) (67k⭐)
