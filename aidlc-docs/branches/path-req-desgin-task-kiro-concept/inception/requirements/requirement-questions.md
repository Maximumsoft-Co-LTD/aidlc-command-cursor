# Kiro-Style AIDLC Simplification - Requirements Questionnaire

> **Instructions**: กรุณาตอบคำถามด้านล่างโดยใส่คำตอบในช่อง `[Answer]:`
> 
> เมื่อตอบเสร็จแล้ว บอก AI ว่า "ตอบเสร็จแล้ว" เพื่อดำเนินการต่อ

---

## Q1: Relationship กับ AIDLC เดิม

ต้องการให้ `.cursor-kiro/` ทำงานแบบไหน?

| Option | Description |
|--------|-------------|
| **A** | **แทนที่ (Replace)** - ลบ `.cursor/rules/aidlc-rules/` และ `.cursor/commands/` เดิม ใช้ `.cursor-kiro/` อย่างเดียว |
| **B** | **อยู่ร่วม (Coexist)** - เก็บ AIDLC เดิมไว้ เพิ่ม `.cursor-kiro/` เป็นทางเลือกใหม่ |
| **C** | **Migrate** - สร้าง `.cursor-kiro/` ใหม่ แล้วค่อย deprecate AIDLC เดิมภายหลัง |

**[Answer]:** 

---

## Q2: Steering Files Content

ต้องการให้แต่ละ steering file มีเนื้อหาอะไร?

### product.md
| Suggestion | Include? |
|------------|----------|
| Product vision & goals | Yes/No |
| User personas | Yes/No |
| Business requirements | Yes/No |
| Success metrics | Yes/No |
| Other (specify below) | |

**[Answer - product.md]:** Yes all of the above

### tech.md
| Suggestion | Include? |
|------------|----------|
| Tech stack (languages, frameworks) | Yes/No |
| Dependencies & versions | Yes/No |
| Coding conventions | Yes/No |
| API standards | Yes/No |
| Other (specify below) | |

**[Answer - tech.md]:** Yes all of the above

### structure.md
| Suggestion | Include? |
|------------|----------|
| Project folder structure | Yes/No |
| File naming conventions | Yes/No |
| Module organization | Yes/No |
| Import patterns | Yes/No |
| Other (specify below) | |

**[Answer - structure.md]:** Yes all of the above

---

## Q3: State/Audit Tracking

ต้องการ tracking แบบไหน?

| Option | Description |
|--------|-------------|
| **A** | **Minimal** - ไม่ต้อง track state/audit (simple like Kiro) |
| **B** | **Branch-based** - ยังคง track แบบ branch-based เหมือนเดิม |
| **C** | **Single file** - track ใน `.cursor-kiro/state.md` file เดียว |

**[Answer]:** A

---

## Q4: Output Location

Artifacts (requirements.md, design.md, tasks.md) เก็บไว้ที่ไหน?

| Option | Description |
|--------|-------------|
| **A** | `.cursor-kiro/specs/` - inside .cursor-kiro folder |
| **B** | `.kiro/specs/` - เหมือน Kiro IDE (standard Kiro location) |
| **C** | `aidlc-docs/kiro/` - ใน aidlc-docs folder เดิม |

**[Answer]:** A (`.cursor-kiro/specs/{feature-name}/requirements.md`)

---

## Q5: Stage Behavior - Requirements Stage

เมื่อ user พิมพ์ request เข้ามา, Requirements stage ควรทำอะไร?

| Feature | Include? |
|---------|----------|
| แปลง natural language → structured requirements | Yes/No |
| สร้าง acceptance criteria (EARS notation) | Yes/No |
| ถามคำถามเพื่อ clarify (ถ้าไม่ชัด) | Yes/No |
| รอ user approve ก่อนไปต่อ | Yes/No |

**[Answer - Requirements]:** 
Yes all of the above
---

## Q6: Stage Behavior - Design Stage

Design stage ควรทำอะไร?

| Feature | Include? |
|---------|----------|
| Architecture overview | Yes/No |
| Component design | Yes/No |
| Data models / schemas | Yes/No |
| API design | Yes/No |
| Tech stack decisions | Yes/No |
| Mermaid diagrams | Yes/No |

**[Answer - Design]:** 
Yes all of the above
---

## Q7: Stage Behavior - Task Stage

Task stage ควรทำอะไร?

| Feature | Include? |
|---------|----------|
| Break down into discrete tasks | Yes/No |
| Sequence tasks by dependencies | Yes/No |
| Generate checklist format | Yes/No |
| Auto-execute tasks when approved | Yes/No |
| Generate tests per task | Yes/No |

**[Answer - Task]:** 
Yes all of the above
---

## Q8: Command Behavior

`/aidlc` command ควรทำงานอย่างไร?

| Feature | Include? |
|---------|----------|
| Auto-detect new vs resume | Yes/No |
| Show progress between stages | Yes/No |
| Allow skip to specific stage | Yes/No |
| Allow re-run stage | Yes/No |

**[Answer - Command]:** 
สร้าง command verion ใหม่ขึ้น มา 
- /aidlc-requirements
- /aidlc-design
- /aidlc-task
- /aidlc-steering
---

## Q9: Additional Features

มี feature อื่นๆ ที่ต้องการเพิ่มหรือไม่?

**[Answer]:** 
No
---

## Q10: Priority / Timeline

ต้องการ implement ทั้งหมดเลย หรือ MVP ก่อน?

| Option | Description |
|--------|-------------|
| **A** | **MVP** - เริ่มจาก core features (3 stages + steering) แล้วค่อยเพิ่ม |
| **B** | **Full** - implement ทุก feature ที่เลือกไว้ทั้งหมด |

**[Answer]:** 
A
---

## Summary (AI filled)

| Aspect | Your Answer |
|--------|-------------|
| Relationship | Coexist (implied - new commands alongside existing) |
| Steering Files | All features for product.md, tech.md, structure.md |
| State Tracking | A - Minimal (no tracking, simple like Kiro) |
| Output Location | `.cursor-kiro/specs/{feature-name}/` |
| Requirements Stage | All features (natural language → EARS, clarify, approve) |
| Design Stage | All features (architecture, components, data, API, Mermaid) |
| Task Stage | All features (breakdown, sequence, checklist, auto-execute, tests) |
| Command Behavior | 4 new commands: /aidlc-requirements, /aidlc-design, /aidlc-task, /aidlc-steering |
| Additional Features | None |
| Priority | A - MVP first |

---

> **เมื่อตอบเสร็จแล้ว** บอก AI ว่า "ตอบเสร็จแล้ว" หรือ "done" เพื่อดำเนินการต่อ

