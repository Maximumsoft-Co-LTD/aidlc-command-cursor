# Business Rules: Unit 1 - Core Infrastructure

## Overview

Business rules ที่ govern การทำงานของ Core Infrastructure components

---

## State Management Rules

### BR-SM-001: State File Location
```
RULE: STATE_FILE_LOCATION
    condition: Always
    action: State file MUST be at "aidlc-docs/aidlc-state.md"
    enforcement: Hardcoded path in StateManager
```

### BR-SM-002: State File Format
```
RULE: STATE_FILE_FORMAT
    condition: When saving state
    action: State MUST be in Markdown format with YAML-like structure
    enforcement: Use consistent template
    
TEMPLATE:
# AI-DLC State Tracking

## Project Information
- **Project Name**: {projectName}
- **Project Type**: {Greenfield|Brownfield}
- **Start Date**: {ISO8601 timestamp}
- **Current Stage**: {stageName}

## Stage Progress
### 🔵 INCEPTION PHASE
- [x|] Stage Name

### 🟢 CONSTRUCTION PHASE
- [x|] Stage Name
```

### BR-SM-003: Stage Completion Order
```
RULE: STAGE_ORDER_ENFORCEMENT
    condition: When marking stage complete
    action: Stage can only be marked complete if:
        1. All prerequisite stages are complete
        2. Current stage matches expected next stage
    enforcement: Check prerequisites before marking
```

### BR-SM-004: No Backward Transitions
```
RULE: NO_BACKWARD_TRANSITIONS
    condition: When transitioning stages
    action: Cannot transition to a previously completed stage
    exception: User explicitly requests restart
    enforcement: Check completedStages array
```

### BR-SM-005: Project Type Immutability
```
RULE: PROJECT_TYPE_IMMUTABLE
    condition: After initial detection
    action: Project type (greenfield/brownfield) cannot change
    enforcement: Set once in state, never modified
```

---

## Audit Logging Rules

### BR-AL-001: Mandatory Logging
```
RULE: MANDATORY_AUDIT_LOGGING
    condition: Every user input and AI action
    action: MUST be logged with timestamp
    enforcement: All commands call logUserInput/logAIAction
    
LOGGED_EVENTS:
- User input (complete raw input)
- AI responses
- Stage transitions
- Approvals/rejections
- Errors
```

### BR-AL-002: Complete Raw Input
```
RULE: COMPLETE_RAW_INPUT
    condition: When logging user input
    action: Log COMPLETE user input exactly as provided
    prohibition: Never summarize or paraphrase
    enforcement: Pass input directly to logger
```

### BR-AL-003: Append Only
```
RULE: APPEND_ONLY_AUDIT
    condition: All audit operations
    action: Only append to audit.md, never overwrite
    prohibition: 
        - Never use write() that overwrites
        - Never delete entries
    enforcement: Use appendToFile() function only
```

### BR-AL-004: Timestamp Format
```
RULE: ISO8601_TIMESTAMPS
    condition: All timestamps in audit
    action: Use ISO 8601 format (YYYY-MM-DDTHH:MM:SSZ)
    enforcement: formatTimestamp() function
```

### BR-AL-005: Audit Entry Format
```
RULE: AUDIT_ENTRY_FORMAT
    condition: All audit entries
    action: Use consistent format
    
FORMAT:
## {Stage Name or Interaction Type}
**Timestamp**: {ISO timestamp}
**User Input**: "{Complete raw user input}"
**AI Response**: "{AI's response or action}"
**Context**: {Stage, action, or decision made}

---
```

---

## File Management Rules

### BR-FM-001: Directory Creation
```
RULE: CREATE_PARENT_DIRECTORIES
    condition: When creating a file
    action: Create parent directories if they don't exist
    enforcement: writeFileSafely() creates parents
```

### BR-FM-002: Safe File Operations
```
RULE: SAFE_FILE_OPERATIONS
    condition: All file operations
    action: Check existence before read, create parent before write
    enforcement: Use *Safely() wrapper functions
```

### BR-FM-003: Standard Directory Structure
```
RULE: STANDARD_AIDLC_STRUCTURE
    condition: When initializing project
    action: Create standard aidlc-docs structure
    
STRUCTURE:
aidlc-docs/
├── inception/
│   ├── plans/
│   ├── requirements/
│   ├── user-stories/
│   ├── reverse-engineering/
│   └── application-design/
├── construction/
│   ├── plans/
│   ├── {unit-name}/
│   └── build-and-test/
├── operations/
├── aidlc-state.md
└── audit.md
```

### BR-FM-004: Markdown File Extension
```
RULE: MARKDOWN_FILES
    condition: All AIDLC documents
    action: Use .md extension
    exception: Cursor rules use .mdc extension
```

---

## Workflow Rules

### BR-WF-001: Workspace Detection First
```
RULE: WORKSPACE_DETECTION_FIRST
    condition: Starting AIDLC workflow
    action: Workspace Detection MUST execute first
    enforcement: Check state on /aidlc command
```

### BR-WF-002: Stage Prerequisites
```
RULE: STAGE_PREREQUISITES
    condition: Before executing any stage
    action: All prerequisite stages MUST be complete
    
PREREQUISITES:
- Requirements Analysis: Workspace Detection
- User Stories: Requirements Analysis
- Workflow Planning: Requirements Analysis (+ User Stories if executed)
- Application Design: Workflow Planning
- Units Generation: Application Design
- Functional Design: Units Generation
- Code Generation: Design stages (as applicable)
- Build and Test: Code Generation
```

### BR-WF-003: Conditional Stage Skip
```
RULE: CONDITIONAL_STAGE_SKIP
    condition: Stages marked as conditional
    action: Skip if conditions not met
    
CONDITIONS:
- Reverse Engineering: Skip if greenfield
- User Stories: Skip if simple/internal change
- Infrastructure Design: Skip if no infra changes
- NFR stages: Skip if no NFR requirements
```

### BR-WF-004: User Approval Required
```
RULE: USER_APPROVAL_REQUIRED
    condition: After completing stage artifacts
    action: Present completion message and wait for explicit approval
    prohibition: Never auto-proceed without approval
    exception: Workspace Detection (informational only)
```

### BR-WF-005: Per-Unit Loop
```
RULE: PER_UNIT_LOOP
    condition: CONSTRUCTION phase
    action: Execute design + code stages for each unit before moving to next unit
    enforcement: Track current unit in state
    
LOOP:
FOR EACH unit IN units:
    execute Functional Design (if applicable)
    execute NFR Requirements (if applicable)
    execute NFR Design (if applicable)
    execute Infrastructure Design (if applicable)
    execute Code Generation
```

---

## Validation Rules

### BR-VL-001: Mermaid Syntax Validation
```
RULE: VALIDATE_MERMAID
    condition: Before saving document with Mermaid
    action: Validate Mermaid syntax
    handling: If invalid, show error and do not save
```

### BR-VL-002: State Consistency
```
RULE: STATE_CONSISTENCY
    condition: When loading state
    action: Validate state structure is valid
    handling: If corrupt, offer recovery options
```

### BR-VL-003: Plan Checkbox Tracking
```
RULE: PLAN_CHECKBOX_TRACKING
    condition: After completing any plan step
    action: IMMEDIATELY mark checkbox as [x]
    enforcement: Same interaction where work is completed
```

---

## Error Handling Rules

### BR-EH-001: File Not Found
```
RULE: FILE_NOT_FOUND_HANDLING
    condition: When expected file doesn't exist
    action: Return null/empty, do not throw
    exception: State file missing = new project
```

### BR-EH-002: Write Permission Error
```
RULE: WRITE_PERMISSION_ERROR
    condition: When cannot write to workspace
    action: Display clear error with suggested fix
    message: "Error: Cannot write to workspace. Please check permissions."
```

### BR-EH-003: State Corruption
```
RULE: STATE_CORRUPTION_HANDLING
    condition: When state file is invalid
    action: Offer options: start fresh or restore from backup
    message: "Warning: State file corrupted. Starting fresh or restore from backup?"
```

---

## Document History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-15 | Initial business rules document |

