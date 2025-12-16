# Requirements: Kiro-Style Simplified AIDLC

**Feature**: Kiro-Style Simplified Workflow  
**Branch**: path/req-desgin-task-kiro-concept  
**Created**: 2025-12-16  
**Status**: ✅ Approved

---

## 1. Overview

สร้างระบบ AIDLC แบบ simplified ที่ได้แรงบันดาลใจจาก [Kiro](https://kiro.dev/) โดยมี 3 stages หลัก และ steering rules สำหรับ context management

### 1.1 Goals
- ลดความซับซ้อนจาก 13 stages → 3 stages
- ใช้งานง่าย เข้าใจได้ทันที
- ไม่ต้อง track state/audit (minimal overhead)
- Steering rules ช่วยให้ AI เข้าใจ context ของ project

---

## 2. Functional Requirements

### FR-001: Folder Structure
**WHEN** user starts using Kiro-style AIDLC  
**THEN** system SHALL create `.cursor-kiro/` folder with structure:

```
.cursor-kiro/
├── steering/                 # Steering rules (context)
│   ├── product.md           # Product context
│   ├── tech.md              # Technical context
│   └── structure.md         # Project structure context
├── commands/                 # Cursor commands
│   ├── aidlc-requirements.md
│   ├── aidlc-design.md
│   ├── aidlc-task.md
│   └── aidlc-steering.md
└── specs/                    # Generated specs per feature
    └── {feature-name}/
        ├── requirements.md
        ├── design.md
        └── tasks.md
```

### FR-002: Steering Files

#### FR-002.1: product.md
**SHALL** contain:
- Product vision & goals
- User personas
- Business requirements
- Success metrics

#### FR-002.2: tech.md
**SHALL** contain:
- Tech stack (languages, frameworks)
- Dependencies & versions
- Coding conventions
- API standards

#### FR-002.3: structure.md
**SHALL** contain:
- Project folder structure
- File naming conventions
- Module organization
- Import patterns

### FR-003: Commands

#### FR-003.1: /aidlc-requirements
**WHEN** user invokes `/aidlc-requirements {feature description}`  
**THEN** system SHALL:
1. แปลง natural language → structured requirements
2. สร้าง acceptance criteria (EARS notation)
3. ถามคำถามเพื่อ clarify (ถ้าไม่ชัด)
4. รอ user approve ก่อนไปต่อ
5. Save to `.cursor-kiro/specs/{feature-name}/requirements.md`

#### FR-003.2: /aidlc-design
**WHEN** user invokes `/aidlc-design`  
**THEN** system SHALL:
1. Load requirements from current feature
2. Generate:
   - Architecture overview
   - Component design
   - Data models / schemas
   - API design
   - Tech stack decisions
   - Mermaid diagrams
3. รอ user approve
4. Save to `.cursor-kiro/specs/{feature-name}/design.md`

#### FR-003.3: /aidlc-task
**WHEN** user invokes `/aidlc-task`  
**THEN** system SHALL:
1. Load requirements + design from current feature
2. Break down into discrete tasks
3. Sequence tasks by dependencies
4. Generate checklist format
5. Generate tests per task
6. รอ user approve
7. Auto-execute tasks when approved
8. Save to `.cursor-kiro/specs/{feature-name}/tasks.md`

#### FR-003.4: /aidlc-steering
**WHEN** user invokes `/aidlc-steering`  
**THEN** system SHALL:
1. Scan codebase to understand context
2. Generate/update steering files:
   - product.md (if product context detected)
   - tech.md (from package.json, dependencies, etc.)
   - structure.md (from folder analysis)
3. Ask user to review and modify

---

## 3. Non-Functional Requirements

### NFR-001: Simplicity
- No state tracking files
- No audit logging
- Minimal overhead

### NFR-002: Compatibility
- Coexist with existing AIDLC (`.cursor/rules/aidlc-rules/`)
- Independent operation

### NFR-003: Output Format
- All specs in Markdown format
- Mermaid diagrams for visual content
- Checklist format for tasks (`- [ ]` syntax)

---

## 4. Acceptance Criteria

### AC-001: Folder Creation
- [ ] `.cursor-kiro/` folder created successfully
- [ ] All subfolders (steering, commands, specs) created
- [ ] Template steering files generated

### AC-002: Commands Work
- [ ] `/aidlc-requirements` generates requirements.md
- [ ] `/aidlc-design` generates design.md
- [ ] `/aidlc-task` generates tasks.md with checklist
- [ ] `/aidlc-steering` generates/updates steering files

### AC-003: Flow Works
- [ ] Requirements → Design → Task flow works sequentially
- [ ] Each stage waits for approval before proceeding
- [ ] Tasks auto-execute after approval

---

## 5. Out of Scope (MVP)

- Branch-based tracking
- Audit logging
- Multi-repo support
- Complex state management
- Operations phase

---

## 6. Dependencies

- Cursor IDE with commands support
- Markdown rendering capability

---

## 7. Approval

**Requirements approved**: ✅ Approved (2025-12-16)

---

> **Next Stage**: Design

