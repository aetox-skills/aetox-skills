---
name: doc-standard
description: >
  ใช้เมื่อเขียนหรืออัปเดตเอกสารทางเทคนิคภาษาไทย — ALL tasks เกี่ยวกับการเขียนเอกสาร
  Open Source ใน Obsidian vault, การสร้างบทเรียนสถาปัตยกรรม, หรือเอกสารระดับตำราเรียน
  อ้างอิงจาก BookMind technical_guide.md และ senior-architect-agent discipline
---

# 📖 Doc-Standard — มาตรฐานเอกสารทางเทคนิค

> ไม่ใช่แม่แบบฟอร์แมต แต่เป็น **ชั้นวินัย** สำหรับงานเขียนเอกสาร —
> แยกข้อเท็จจริงจากการอนุมาน, รู้ว่าอะไรยังไม่ยืนยัน, และหยุดเมื่อพอดี

อ้างอิงจาก: `BookMind/docs/technical_guide.md` + `senior-architect-agent`

---

## Operating Rules (กฎ 10 ข้อ — ห้ามละเมิด)

1. **ห้ามเขียนก่อนตรวจสอบ** — ต้อง `webfetch` repo, README, AGENTS.md ก่อนเขียน
2. **ห้ามอ้าง stars/milestones โดยไม่ยืนยัน** — ใช้ตัวเลขจริงจาก GitHub
3. **ห้ามเดาโดยไม่ทำเครื่องหมาย** — ทุกข้อความที่อนุมานต้องกำกับ `[อนุมาน]`
4. **แยกข้อเท็จจริง 4 ระดับ** — Direct, Inferred, Assumed, Unverified (ดู Section Evidence)
5. **ถามก่อนสรุป** — ถ้าขาดข้อมูลสำคัญ ให้ถามผู้ใช้หรือทำเครื่องหมาย `[ยังไม่ยืนยัน]`
6. **ใช้ภาษาไทย** — ยกเว้นชื่อโปรเจค, framework, URL, code
7. **มี "ทำไม" ทุกครั้ง** — อธิบายเหตุผลการออกแบบ ไม่ใช่แค่ "อะไร"
8. **Diagram โยงถึงแหล่ง** — ทุก diagram component ต้องอ้างอิงไฟล์หรือ docs ได้
9. **หยุดเมื่อพอดี** — ไม่ใช่ทุกโปรเจคต้องเขียน 15 sections (ดู Pass Levels)
10. **ห้ามสร้างเอกสารตกแต่ง** — ทุก section ต้องมีประโยชน์ ไม่งั้นตัดทิ้ง

---

## Pass Levels (ระดับความลึกของเอกสาร)

เลือกก่อนเริ่มเขียน:

### 🔍 Quick Note (1-3 sections)
ใช้เมื่อ: โปรเจคเล็ก, low-risk, หรือสำรวจเบื้องต้น
- 1. ภาพรวม (2-3 ย่อหน้า)
- 2. สถาปัตยกรรม (1 diagram หลัก)
- 3. สิ่งที่ได้เรียนรู้ (ตารางสรุป)

### 📄 Standard Chapter (5-8 sections)
ใช้เมื่อ: โปรเจคขนาดกลาง, ต้องการมือส่งต่อให้ AI อ่านได้
- 1. ภาพรวม
- 2. สถาปัตยกรรม
- 3. โครงสร้างไฟล์
- 4. แนวคิดหลัก
- 5. Data Flow
- 6. Design Patterns
- 7. สรุป
- 8. คำถามท้ายบท

### 📘 Full Textbook (10-15 sections)
ใช้เมื่อ: โปรเจคใหญ่, ซับซ้อน, หรือเป็น foundation ของ ecosystem
- ทุก sections ใน Standard +
- 7. Code Walkthrough (วิเคราะห์โค้ดทีละส่วน)
- 8. การเปรียบเทียบ (เทียบกับโปรเจคใกล้เคียง)
- 9. Deep Dive (1-3 หัวข้อ)
- 10. Benchmark/สถิติ
- 11. สรุป
- 12. คำถามท้ายบท

**Pass Promotion Gate:**
- ต้องมี trigger ชัดเจน (เช่น "ผู้ใช้ขอ Full", "พบ 3+ modules ที่เกี่ยวเนื่องกัน")
- ต้องอ้างอิง evidence หรือคำขอผู้ใช้
- ต้องระบุ risk ถ้าอยู่ใน pass ที่ต่ำกว่า

---

## Evidence Strength (ระดับความน่าเชื่อถือของข้อมูล)

ทุกข้อความสำคัญต้องกำกับ:

| ระดับ | เครื่องหมาย | ความหมาย | ตัวอย่าง |
|-------|-----------|---------|---------|
| **Direct** | `[✓]` | ยืนยันจาก repo, README, docs โดยตรง | `[✓] stars: 176k (จาก GitHub)` |
| **Inferred** | `[→]` | อนุมานจากหลักฐาน แต่ยังไม่ยืนยันตรงๆ | `[→] น่าจะใช้ SQLite เพราะเห็น drizzle ใน package.json` |
| **Assumed** | `[?]` | ตั้งสมมติฐานเพื่อให้เขียนต่อได้ | `[?] สมมติว่า session timeout = 30 นาที` |
| **Unverified** | `[!]` | ยังไม่มีหลักฐาน — ต้องกลับมายืนยัน | `[!] ยังไม่ได้อ่านไฟล์ permission.ts` |

ใช้ `ตรวจสอบก่อน: ใช่` สำหรับข้อความที่สำคัญมากและควรให้มนุษย์หรือ AI ในอนาคตตรวจสอบซ้ำ

---

## Checkpoint Gates (ด่านตรวจ)

ผ่านทุกด่านก่อนส่งงาน:

### Gate 1: Intake
- [ ] เลือก Pass Level แล้ว (Quick / Standard / Full)
- [ ] รู้ scope (กี่ sections, ใช้เวลาเท่าไหร่)
- [ ] รู้ว่าไฟล์ output อยู่ที่ไหน
- [ ] หรือ Early Exit: `ไม่จำเป็นต้องเขียนเอกสารเพิ่ม — <เหตุผล>`

### Gate 2: Inspection
- [ ] ดึงข้อมูลจาก repo แล้ว (webfetch GitHub README, AGENTS.md, docs)
- [ ] มี stars, language, license จริง
- [ ] บันทึกข้อจำกัดการตรวจสอบ (เช่น "ยังไม่ได้อ่าน subdirectory X")

### Gate 3: Classification
- [ ] แยกหมวดหมู่ของระบบแล้ว (frontend, backend, database, AI, external, infra)
- [ ] ระบุหมวดที่ยังไม่เห็น (`ไม่พบ`)

### Gate 4: Question
- [ ] ระบุสิ่งที่ยังไม่รู้และสำคัญต่อ architecture
- [ ] หรือเขียนว่า `ไม่มีคำถามที่ส่งผลต่อ architecture`

### Gate 5: Mapping
- [ ] Diagram เชื่อมโยงกับ evidence ได้
- [ ] Components ที่ไม่แน่ใจถูกกำกับ `[→]` `[?]` `[!]`

### Gate 6: Validation (ตอบ 3 คำถาม)
1. **Claim Traceability:** ทุกข้อความสำคัญมีแหล่งอ้างอิงไหม? ถ้าไม่มี → `[!]` หรือตัดทิ้ง
2. **Scope Alignment:** ขอบเขตสุดท้ายตรงกับที่ intake ไว้ไหม? ถ้าขยาย → ระบุสาเหตุ
3. **Handoff Readiness:** มี Unknowns และ Safe Next Actions ไหม? ถ้าไม่มี → เขียนว่า `ไม่มี`

---

## โครงสร้างเอกสาร (Structure)

### 1. ส่วนหัว (Header) — ทุกบท

```markdown
---
tags:
  - opensource
  - หมวด
project: ชื่อโปรเจค
lang: ภาษา
stars: จำนวนดาว (ยืนยันแล้ว [✓])
status: กำลังศึกษา / pending
created: วันที่
updated: วันที่
repo: https://github.com/...
docs: https://...
---

# 📘 เอกสารอธิบายระบบ <ชื่อโปรเจค>
# <ชื่อโปรเจค> — Technical Documentation (v1.0)

> คำคม/สรุปหนึ่งบรรทัด — จับใจความสำคัญ
```

### 2. สารบัญ — ทุกบท

```markdown
## สารบัญ

1. [ภาพรวม](#1-ภาพรวมระบบ)
2. [สถาปัตยกรรม](#2-สถาปัตยกรรม)
3. ...
N. [คำถามท้ายบท](#n-คำถามท้ายบท)
```

### 3. Section Format

```markdown
## 1. ชื่อหัวข้อ — คำอธิบายสั้น

### 1.1 หัวข้อย่อย

เนื้อหา...

**ไฟล์ที่เกี่ยวข้อง:** `path/to/file` → function/class
**ค่าตั้ง:** `config.file` → `KEY = value`
```

---

## รูปแบบการเขียน (Styling)

### Emoji นำหน้า Section

| หัวข้อ | Emoji | ใช้เมื่อ |
|--------|-------|---------|
| ภาพรวม / บทนำ | 📘 | ทุกบท |
| สถาปัตยกรรม | 🏗️ | section สถาปัตยกรรม |
| แนวคิดหลัก | 🧠 | core concepts |
| Data Flow | 🔄 | กระแสข้อมูล |
| เปรียบเทียบ | ⚖️ | comparison tables |
| Deep Dive | 🎓 | concept ลึก |
| Code Walkthrough | 🔬 | วิเคราะห์โค้ด |
| Benchmark | ⚡ | performance, timing |
| สรุป | 📌 | summary |
| คำถามท้ายบท | ❓ | review questions |
| ข้อควรระวัง | ⚠️ | warnings, anti-patterns |
| New Feature | 🆕 | ฟีเจอร์ใหม่ในเวอร์ชั่นล่าสุด |
| Tuning | 💡 | tips การปรับแต่ง |

### Architecture Diagram

```
┌──────────────────────────────────────────────┐
│              Component Name                    │
├──────────────────────────────────────────────┤
│  Sub-component                   [✓] จากไฟล์  │
│  ├── Feature A                   [→] อนุมาน  │
│  ├── Feature B                   [?] สมมติ   │
│  └── Feature C                   [!] ไม่ยืนยัน│
└──────────────────────────────────────────────┘
```

### Data Flow (Vertical)

```
Input
    │
    ▼  Step 1 — คำอธิบาย ⏱️ ~5ms
    │
    ▼  Step 2 — คำอธิบาย ⏱️ ~100ms
    │
Output
```

### ตาราง

```markdown
| ปัจจัย | ตัวเลือก A | ตัวเลือก B |
|--------|-----------|------------|
| **เกณฑ์ 1** | ✅ ดีมาก | ❌ อ่อน |
| **เกณฑ์ 2** | 2.2 GB | 0.3 GB |
```

- หัวตาราง `---` (ไม่ใช่ `===`)
- จัดชิดซ้าย
- ทำตัวหนา column แรก

### Deep Dive (🎓)

```markdown
> 🎓 **Deep Dive: ชื่อหัวข้อ**
> คำอธิบายเชิงลึก — เข้าใจ concept นี้แล้วจะเข้าใจทั้งระบบ
```

หรือ:

```markdown
### 🎓 Deep Dive: ชื่อหัวข้อ

เนื้อหา...
```

### File Reference

```markdown
**ไฟล์ที่เกี่ยวข้อง:** `package/module/file.ts` → `ClassName.method()`
**ค่าตั้ง:** `config.ts` → `KEY = value`
```

### Code Blocks

````markdown
```ภาษา
# คำอธิบายภาษาไทย
code here
```
````

- บอกภาษาทุกครั้ง
- คอมเมนต์เป็นภาษาไทย (ยกเว้นโค้ดจริงจาก repo)

---

## Anti-Patterns (สิ่งที่ไม่ควรทำ)

| ❌ อย่าทำ | ✅ ควรทำ |
|-----------|---------|
| เขียน 15 sections ทุกโปรเจค | เลือก Pass Level ที่เหมาะสม |
| ใช้ stars เก่า | ดึง stars ปัจจุบันจาก GitHub |
| เดาสถาปัตยกรรมโดยไม่อ่านโค้ด | WebFetch repo ก่อนเขียน |
| Diagram สวยแต่โยงไม่ได้ | ทุก component มี `[✓]` `[→]` `[?]` `[!]` |
| ใช้ `การทำงานของระบบคือ...` หลายครั้ง | สั้น ตรงประเด็น |
| เขียนทับไฟล์โดยไม่อ่านก่อน | อ่านไฟล์เก่า → คงของดี → เพิ่มของใหม่ |
| ไม่มีคำถามท้ายบท | มี 3-5 ข้อเสมอ |
| ภาษาอังกฤษปนโดยไม่จำเป็น | ไทยให้มากที่สุด |
| อธิบายแค่ "อะไร" ไม่มี "ทำไม" | มีเหตุผลการออกแบบทุกครั้ง |

---

## Checklist ก่อนส่งงาน

```
Checkpoint Gates:
□ Gate 1: Intake — Pass Level, scope, output path
□ Gate 2: Inspection — repo info, stars, limitations
□ Gate 3: Classification — system areas, missing areas
□ Gate 4: Question — unknowns listed or "None identified"
□ Gate 5: Mapping — diagrams traceable to evidence
□ Gate 6: Validation — 3 questions answered

Style Check:
□ ภาษาไทยทั้งหมด (ยกเว้นชื่อ, code, URL)
□ Emoji นำหน้าทุก section
□ Architecture diagram มีอยู่
□ ตารางใช้สำหรับเปรียบเทียบ
□ Code blocks มีระบุภาษา
□ Deep Dive สำหรับ concept สำคัญ
□ File/Config references ท้าย section
□ "ทำไม" อธิบายเหตุผล

Content Check:
□ Stars/language/license เป็นปัจจุบัน [✓]
□ [→] [✓] [?] [!] ถูกใช้ถูกต้อง
□ Diagram ดึงมาจาก repo structure จริง
□ คำถามท้ายบท 3-5 ข้อ
□ Unknowns เขียนไว้ชัดเจน
```

---

## Templates (Quick Reference)

### Quick Note Template
```markdown
# 📘 Quick: <ชื่อโปรเจค>
> หนึ่งบรรทัด

## 1. ภาพรวม
...

## 2. สถาปัตยกรรม
```
diagram
```

## 3. สิ่งที่ได้เรียนรู้
| สิ่งที่เรียน | รายละเอียด |
|-------------|-----------|
| ... | ... |
```

### Standard Chapter Template
```markdown
# 📘 <ชื่อโปรเจค> — Technical Docs
> หนึ่งบรรทัด

## สารบัญ
...

## 1. ภาพรวมระบบ
## 2. สถาปัตยกรรม
## 3. โครงสร้างไฟล์
## 4. แนวคิดหลัก
## 5. Data Flow
## 6. Design Patterns
## 7. สรุป
## 8. คำถามท้ายบท
```
