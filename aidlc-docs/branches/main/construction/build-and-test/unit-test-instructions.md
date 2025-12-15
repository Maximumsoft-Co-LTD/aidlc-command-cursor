# Unit Test Instructions: AIDLC Command System

## Overview

AIDLC Command System ใช้ manual testing ผ่าน Cursor Chat เนื่องจากเป็น rules-based system

---

## Test Strategy

### Approach
เนื่องจาก Cursor Rules ไม่มี automated testing framework  
เราใช้ **Manual Testing** ผ่าน scenarios ใน Cursor Chat

### Test Categories
1. **Command Recognition** - ตรวจสอบว่า commands ถูก recognize
2. **Workflow Flow** - ตรวจสอบ workflow progression
3. **State Management** - ตรวจสอบ state file updates
4. **Error Handling** - ตรวจสอบ error scenarios

---

## Test Cases

### TC-01: Main Command Recognition

| Test | Command | Expected Result |
|------|---------|-----------------|
| TC-01.1 | `/aidlc` | Shows welcome or resume message |
| TC-01.2 | `/aidlc-init` | Creates folder structure |
| TC-01.3 | `/aidlc-status` | Shows current status |

**Steps:**
1. Open Cursor Chat
2. Type command
3. Verify response matches expected

### TC-02: Project Initialization

| Step | Action | Expected |
|------|--------|----------|
| 1 | New empty workspace | - |
| 2 | Type `/aidlc-init` | Folder structure created |
| 3 | Check `aidlc-docs/` | State and audit files exist |
| 4 | Type `/aidlc-status` | Shows greenfield project |

### TC-03: Workflow Progression

| Step | Command | Expected State |
|------|---------|----------------|
| 1 | `/aidlc-init` | Workspace Detection ✅ |
| 2 | `/aidlc-requirements` | Requirements Analysis running |
| 3 | Answer questions | Requirements complete |
| 4 | `/aidlc-status` | Shows requirements ✅ |

### TC-04: Inception Commands

| Test | Command | Expected |
|------|---------|----------|
| TC-04.1 | `/aidlc-reverse` | Shows "not needed" for greenfield |
| TC-04.2 | `/aidlc-requirements` | Generates questions |
| TC-04.3 | `/aidlc-stories` | Generates personas and stories |
| TC-04.4 | `/aidlc-plan` | Creates execution plan |
| TC-04.5 | `/aidlc-design` | Creates design artifacts |
| TC-04.6 | `/aidlc-units` | Creates units of work |

### TC-05: Construction Commands

| Test | Command | Expected |
|------|---------|----------|
| TC-05.1 | `/aidlc-functional` | Creates functional design |
| TC-05.2 | `/aidlc-nfr` | Creates NFR documents |
| TC-05.3 | `/aidlc-infra` | Creates infra design |
| TC-05.4 | `/aidlc-code` | Creates code gen plan |
| TC-05.5 | `/aidlc-build` | Creates build instructions |

### TC-06: State Management

| Test | Action | Expected |
|------|--------|----------|
| TC-06.1 | Complete stage | State file updated |
| TC-06.2 | Resume workflow | Continues from last stage |
| TC-06.3 | View status | Shows correct progress |

### TC-07: Error Handling

| Test | Scenario | Expected |
|------|----------|----------|
| TC-07.1 | `/aidlc` without init | Prompts to initialize |
| TC-07.2 | Skip required stage | Shows prerequisite error |
| TC-07.3 | Corrupted state | Offers recovery |

---

## Test Execution Log

```markdown
## Test Run: {Date}

### Environment
- Cursor Version: {version}
- OS: {os}
- Workspace: {path}

### Results

| Test ID | Status | Notes |
|---------|--------|-------|
| TC-01.1 | PASS/FAIL | {notes} |
| TC-01.2 | PASS/FAIL | {notes} |
...
```

---

## Document History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-15 | Initial test instructions |

