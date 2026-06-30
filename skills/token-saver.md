# Token Saver ⚡

CLI proxy ที่กรองและย่อ output bash command ก่อนส่งถึง LLM context ประหยัด token **55-90%**

## Use When

- สั่ง `git`, `pytest`, `cargo test`, `npm install`, `pip install`, `find`, `docker`, `curl`
- ต้องการลด token waste จาก progress bar, passed test boilerplate, file lists ยาว
- ทำงานกับ OpenCode / Claude Code / Cursor / Codex / AI tool ใดๆ ที่เรียก bash

## Installation

```bash
# OpenCode plugin (auto-rewrite)
rtk init -g --opencode

# Claude Code hook
rtk init -g

# Agent-specific
rtk init -g --agent cursor
rtk init -g --codex
```

## Usage Rules

| ประเภท | คำสั่ง | ใช้ rtk? |
|--------|--------|:--------:|
| Test | `pytest`, `cargo test` | ✅ (fail → อ่าน tee file) |
| Install | `npm/pnpm/pip install` | ✅ |
| Git | `status`, `add`, `commit`, `log`, `diff` | ✅ |
| Find | `find` | ✅ |
| Docker | `ps`, `build`, `images` | ✅ |
| Curl | `curl` | ✅ |
| JSON | `json file.json` | ✅ |
| TypeScript | `tsc --noEmit` | ✅ (แต่ถ้า fail → **ต้องอ่าน tee file**) |
| Git diff review | `git diff` (ต้องการดู code) | ❌ |
| echo, which, Test-Path | | ❌ |
| Read/Glob/Grep tools | | ❌ (ไม่ใช่ bash) |

## ⚠️ Tee Recovery

เมื่อ `rtk` filter output แล้ว command **fail**:
1. RTK แสดง `[full output: ~/.local/share/rtk/tee/xxx.log]`
2. อ่านไฟล์นั้นเพื่อดู error/output เต็ม
3. แก้บั๊กตาม error จริง

```toml
[tee]
enabled = true
mode = "failures"
```

## Analytics

```bash
rtk gain           # ดู token savings
rtk gain --history # ประวัติล่าสุด
```
