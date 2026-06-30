# ⚡ Token Saver — RTK Protocol

> **AI Agent Protocol:** Load this skill before running any bash command this session.
> RTK intercepts bash commands and strips noise before output reaches the LLM.
> **Saves 55-90%** of tokens wasted on progress bars, passed test boilerplate, long file lists.
> Platform-agnostic: works with OpenCode, Claude Code, Codex, Cursor, Gemini CLI, or any AI coding tool.

## Iron Rules

### ✅ Always use `rtk` prefix

| Command | Use | Reason |
|---------|-----|--------|
| `git status/log/diff/add/commit/push` | `rtk git ...` | compresses 53-96% |
| `pytest`, `cargo test`, `go test`, `jest`, `vitest` | `rtk pytest/cargo test ...` | strip passed boilerplate, show only failures |
| `npm/pnpm/pip install` | `rtk npm/pnpm/pip install` | progress bars = garbage tokens |
| `find ...` | `rtk find ...` | tree output instead of flat list |
| `docker ps/images/build` | `rtk docker ...` | strip SHA/container IDs |
| `curl ...` | `rtk curl ...` | auto detect JSON → schema output |
| `json file.json` | `rtk json ...` | compact / keys-only mode |
| `tsc --noEmit`, `tsc` | `rtk tsc` | large error output (if fail → tee recovery) |

### ❌ Skip rtk

| Command | Reason |
|---------|--------|
| `echo`, `cp`, `mv`, `mkdir`, `which`, `Test-Path` | output = 1-2 tokens |
| `git diff` when reviewing code | need full diff context |

### 🚨 Bypass when raw output needed

```bash
rtk proxy <cmd>   # passthrough — no filtering, still tracks stats
```

---

## ⚡ Tee Recovery Protocol (CRITICAL)

When a filtered command **fails**, RTK saves the full unfiltered output to a tee file.

```
1. Run: rtk tsc --noEmit
2. Output: FAILED: 3 errors  [full output: /path/to/rtk/tee/xxx.log]
3. AI MUST: Read that file → see full error → fix code
4. NEVER: guess the error, ignore the tee file, or ask user to re-run
```

**Tee paths:**
| OS | Path |
|----|------|
| Windows | `C:\Users\<user>\AppData\Local\rtk\tee\` |
| Linux/Mac | `~/.local/share/rtk/tee/` |

**Config:**
```toml
[tee]
enabled = true
mode = "failures"
max_files = 20
max_file_size = 1048576
```

---

## Agent Workflow

```
Load skill → About to run bash?
  ├─ Long output / noise → prefix with rtk
  ├─ Small output / data → run directly
  └─ Command failed?
       ├─ YES → Read tee file → fix from real error
       └─ NO  → ✓ Tokens saved
```

---

## Prerequisites

```bash
rtk --version   # must show v0.34.x+
rtk gain        # check token savings
```

## Analytics

```bash
rtk gain              # summary stats
rtk gain --history    # recent commands
```

---

> **Bottom line:** Spend tokens where it matters (failures → tee recovery)
> Save where it doesn't (passes → compact). Good agent = uses rtk + recovers from tee.
