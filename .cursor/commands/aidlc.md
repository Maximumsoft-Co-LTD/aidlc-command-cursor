# /aidlc - AI Development Life Cycle

Execute the AIDLC workflow based on user request.

## Instructions

When this command is invoked:

1. **Load the core workflow**: Read and follow rules from `aidlc-rules/aws-aidlc-rules/core-workflow.mdc`
2. **Classify the request** using the Request Classification Matrix
3. **Execute appropriate workflow** based on classification

## 🔴 CRITICAL RULES

### Questions MUST Be Files, NOT Chat
- **NEVER** ask questions directly in chat
- **ALWAYS** create question files: `aidlc-docs/branches/{branch}/inception/{stage}-questions.md`
- Use multiple-choice format from `common/question-format-guide.md`
- Wait for user to complete file before proceeding

### Request Classification

| Type | Description | Action |
|------|-------------|--------|
| ❓ Question | About AIDLC, how things work | Answer directly |
| 📋 Work Request | Add, modify, fix, create, implement | Follow AIDLC workflow |
| 📊 Status Check | Check status, what's next | Read state file and respond |
| 🔧 Fix/Resume | Post-completion errors | Fix/Resume flow |

## Workflow Phases

```
🔵 INCEPTION PHASE (WHAT and WHY)
├── Workspace Detection (ALWAYS)
├── Reverse Engineering (brownfield only)
├── Requirements Analysis (ALWAYS)
├── User Stories (CONDITIONAL)
├── Workflow Planning (ALWAYS)
├── Application Design (CONDITIONAL)
└── Units Generation (CONDITIONAL)

🟢 CONSTRUCTION PHASE (HOW)
├── Per-Unit Loop:
│   ├── Functional Design (CONDITIONAL)
│   ├── NFR Requirements (CONDITIONAL)
│   ├── NFR Design (CONDITIONAL)
│   ├── Infrastructure Design (CONDITIONAL)
│   └── Code Generation (ALWAYS)
└── Build and Test (ALWAYS)

🟡 OPERATIONS PHASE (placeholder)
└── Future: deployment & monitoring
```

## Directory Structure

```
aidlc-docs/
├── audit/{branch}.md         # Audit trail
├── state/{branch}.md         # Current state
└── branches/{branch}/
    ├── inception/            # Inception artifacts
    │   ├── plans/
    │   ├── requirements/
    │   ├── user-stories/
    │   └── application-design/
    └── construction/         # Construction artifacts
        ├── {unit-name}/
        └── build-and-test/
```

## Usage Examples

### Start New Project
```
/aidlc สร้าง REST API สำหรับ user authentication
```

### Resume Work
```
/aidlc
```

### Jump to Stage
```
/aidlc skip to code generation
```

### Re-run Stage
```
/aidlc re-run requirements analysis
```

## Key Principles

- **Adaptive Execution**: Only execute stages that add value
- **User Control**: User can request stage inclusion/exclusion
- **Audit Trail**: Log ALL user inputs in branch audit file
- **Questions = Files**: ALL clarifying questions in question files, NEVER in chat
- **Branch-Based**: Separate state/artifacts per Git branch

## Related Commands

| Command | Description |
|---------|-------------|
| `/aidlc-status` | View current workflow status |
| `/aidlc-changelog` | Update CHANGELOG.md |
| `/aidlc-multi-repo` | Configure related projects |
