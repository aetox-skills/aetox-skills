# Token Saver ⚡

CLI proxy ที่กรองและย่อ output bash command ก่อนส่งถึง LLM context ประหยัด token **55-90%**

## Use When

- สั่ง `git`, `pytest`, `cargo test`, `npm install`, `pip install`, `find`, `docker`, `curl`
- ต้องการลด token waste จาก progress bar, passed test boilerplate, file lists ยาว
- ทำงานกับ OpenCode / Claude Code / Cursor / Codex / AI tool ใดๆ ที่เรียก bash

## Prerequisites

```bash
rtk --version   # ต้องมี rtk ใน PATH
rtk gain        # ดู token savings
```

เครื่องของ Mike: ติดตั้งแล้วที่ `C:\Users\Gigabyte\.config\opencode\plugins\rtk.ts` (OpenCode plugin)

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
| ต้องการ output ดิบ (passthrough) | `rtk proxy <cmd>` | ใช้แทน rtk |

## ⚠️ Tee Recovery

เมื่อ `rtk` filter output แล้ว command **fail**:
1. RTK แสดง `[full output: ...tee/xxx.log]`
2. **อ่านไฟล์นั้น**เพื่อดู error/output เต็ม (อย่า ignore)
3. แก้บั๊กตาม error จริง

**Windows path:** `C:\Users\<user>\AppData\Local\rtk\tee\`
**Linux/Mac:** `~/.local/share/rtk/tee/`

นี่คือหัวใจของ RTK — success = ประหยัด token, fail = recover error เต็ม

```toml
[tee]
enabled = true
mode = "failures"
```

## How Agents Use This Skill

เมื่อ agent โหลด skill นี้ (`skill("rtk")` หรือเปิด `token-saver.md`):
1. **ทุก bash command ที่ output ยาว → ใช้ `rtk` prefix** (หรือปล่อยให้ plugin auto-rewrite)
2. **ตอน fail → อ่าน tee file ก่อนสรุป** ห้ามเดาว่า error คืออะไร
3. **Install / Git / Test / Find / Docker / Curl → rtk ทุกครั้ง**
4. **tsc / pytest / cargo test ที่ fail → tee recovery** (สำคัญมาก)

## Analytics

```bash
rtk gain           # ดู token savings
rtk gain --history # ประวัติล่าสุด
```
