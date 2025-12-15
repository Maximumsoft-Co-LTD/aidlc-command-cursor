# Business Logic Model: Unit 1 - Core Infrastructure

## Overview

Unit 1 provides core infrastructure logic ที่ถูกใช้โดยทุก commands ใน AIDLC system

---

## Component 1: StateManager

### Business Logic

#### BL-SM-01: Load State
```
FUNCTION loadState():
    IF file "aidlc-docs/aidlc-state.md" EXISTS:
        content = READ_FILE("aidlc-docs/aidlc-state.md")
        state = PARSE_MARKDOWN_FRONTMATTER(content)
        RETURN state
    ELSE:
        RETURN null  // No existing state
```

#### BL-SM-02: Save State
```
FUNCTION saveState(state):
    content = FORMAT_STATE_AS_MARKDOWN(state)
    WRITE_FILE("aidlc-docs/aidlc-state.md", content)
    RETURN true
```

#### BL-SM-03: Get Current Stage
```
FUNCTION getCurrentStage():
    state = loadState()
    IF state IS null:
        RETURN null
    RETURN state.currentStage
```

#### BL-SM-04: Mark Stage Complete
```
FUNCTION markStageComplete(stageName):
    state = loadState()
    IF stageName NOT IN state.completedStages:
        ADD stageName TO state.completedStages
    state.currentStage = getNextStage(stageName)
    saveState(state)
    RETURN true
```

#### BL-SM-05: Get Next Stage
```
FUNCTION getNextStage(currentStage):
    stageOrder = [
        "workspace-detection",
        "reverse-engineering",      // Conditional
        "requirements-analysis",
        "user-stories",             // Conditional
        "workflow-planning",
        "application-design",       // Conditional
        "units-generation",         // Conditional
        "functional-design",        // Per-unit
        "nfr-requirements",         // Per-unit, Conditional
        "nfr-design",               // Per-unit, Conditional
        "infrastructure-design",    // Per-unit, Conditional
        "code-generation",          // Per-unit
        "build-and-test"
    ]
    
    currentIndex = FIND_INDEX(stageOrder, currentStage)
    nextStage = stageOrder[currentIndex + 1]
    
    // Check if next stage should be skipped
    WHILE shouldSkip(nextStage):
        currentIndex = currentIndex + 1
        nextStage = stageOrder[currentIndex + 1]
    
    RETURN nextStage
```

---

## Component 2: AuditLogger

### Business Logic

#### BL-AL-01: Log User Input
```
FUNCTION logUserInput(input, context):
    timestamp = formatTimestamp()
    entry = FORMAT_AUDIT_ENTRY(
        timestamp: timestamp,
        type: "USER_INPUT",
        input: input,
        context: context
    )
    APPEND_TO_FILE("aidlc-docs/audit.md", entry)
    RETURN true
```

#### BL-AL-02: Log AI Action
```
FUNCTION logAIAction(action, details):
    timestamp = formatTimestamp()
    entry = FORMAT_AUDIT_ENTRY(
        timestamp: timestamp,
        type: "AI_ACTION",
        action: action,
        details: details
    )
    APPEND_TO_FILE("aidlc-docs/audit.md", entry)
    RETURN true
```

#### BL-AL-03: Log Stage Transition
```
FUNCTION logStageTransition(fromStage, toStage):
    timestamp = formatTimestamp()
    entry = FORMAT_AUDIT_ENTRY(
        timestamp: timestamp,
        type: "STAGE_TRANSITION",
        from: fromStage,
        to: toStage
    )
    APPEND_TO_FILE("aidlc-docs/audit.md", entry)
    RETURN true
```

#### BL-AL-04: Format Timestamp
```
FUNCTION formatTimestamp():
    now = GET_CURRENT_TIME()
    RETURN FORMAT_ISO8601(now)  // e.g., "2025-12-15T00:00:00Z"
```

#### BL-AL-05: Append Only Rule
```
RULE: NEVER_OVERWRITE_AUDIT
    description: "Audit log must be append-only"
    enforcement:
        - Always use APPEND_TO_FILE, never WRITE_FILE
        - If file doesn't exist, create with header first
        - Never delete or modify existing entries
```

---

## Component 3: FileManager

### Business Logic

#### BL-FM-01: Create Directory Structure
```
FUNCTION createDirectoryStructure():
    directories = [
        "aidlc-docs/",
        "aidlc-docs/inception/",
        "aidlc-docs/inception/plans/",
        "aidlc-docs/inception/requirements/",
        "aidlc-docs/inception/user-stories/",
        "aidlc-docs/inception/reverse-engineering/",
        "aidlc-docs/inception/application-design/",
        "aidlc-docs/construction/",
        "aidlc-docs/construction/plans/",
        "aidlc-docs/construction/build-and-test/",
        "aidlc-docs/operations/"
    ]
    
    FOR EACH dir IN directories:
        CREATE_DIRECTORY_IF_NOT_EXISTS(dir)
    
    RETURN true
```

#### BL-FM-02: File Exists Check
```
FUNCTION fileExists(path):
    RETURN CHECK_FILE_EXISTS(path)
```

#### BL-FM-03: Read File Safely
```
FUNCTION readFileSafely(path):
    IF NOT fileExists(path):
        RETURN null
    content = READ_FILE(path)
    RETURN content
```

#### BL-FM-04: Write File Safely
```
FUNCTION writeFileSafely(path, content):
    parentDir = GET_PARENT_DIRECTORY(path)
    IF NOT directoryExists(parentDir):
        CREATE_DIRECTORY(parentDir)
    WRITE_FILE(path, content)
    RETURN true
```

#### BL-FM-05: Append to File
```
FUNCTION appendToFile(path, content):
    IF NOT fileExists(path):
        WRITE_FILE(path, content)
    ELSE:
        existingContent = READ_FILE(path)
        newContent = existingContent + "\n" + content
        WRITE_FILE(path, newContent)
    RETURN true
```

---

## State Machine: Workflow Progression

```
┌──────────────────┐
│   INCEPTION      │
│                  │
│  ┌────────────┐  │
│  │ Workspace  │──┼──→ Requirements ──→ Stories ──→ Planning
│  │ Detection  │  │           │             │           │
│  └────────────┘  │           ▼             ▼           ▼
│                  │      (brownfield?)  (needed?)    Design
│                  │           │             │           │
│  ┌────────────┐  │           ▼             │           ▼
│  │  Reverse   │◀─┼───── if yes            │        Units
│  │Engineering │  │                         │           │
│  └────────────┘  │                         │           │
└──────────────────┘                         │           │
                                             │           │
┌──────────────────┐                         │           │
│  CONSTRUCTION    │◀────────────────────────┴───────────┘
│                  │
│  For Each Unit:  │
│  ┌────────────┐  │
│  │ Functional │──┼──→ NFR Req ──→ NFR Design ──→ Code Gen
│  │  Design    │  │                                   │
│  └────────────┘  │                                   ▼
│                  │                              Build & Test
│                  │
└──────────────────┘
```

---

## Document History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-15 | Initial business logic model |

