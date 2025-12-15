# /aidlc - Main Entry Command

Main entry point for AIDLC (AI Development Life Cycle) workflow.

## What This Command Does

When you use this command, the AI will:

1. **Detect Workspace State**
   - Check for existing `aidlc-docs/state/{branch}.md`
   - Scan for existing source code
   - Determine if Greenfield (new) or Brownfield (existing code)

2. **For New Projects**
   - Create `aidlc-docs/` folder structure
   - Initialize `state/{branch}.md` and `audit/{branch}.md`
   - Proceed to Requirements Analysis

3. **For Resume**
   - Load existing state
   - Continue from last stage
   - Show current progress

## AIDLC Workflow Overview

```
🔵 INCEPTION PHASE
├── Workspace Detection → Requirements → Stories → Planning → Design → Units

🟢 CONSTRUCTION PHASE  
├── Functional Design → NFR → Infrastructure → Code Generation → Build & Test

🟡 OPERATIONS PHASE
└── (Placeholder for future)
```

## Related Commands

- `/aidlc-init` - Initialize project only
- `/aidlc-status` - View current status
- `/aidlc-requirements` - Start requirements analysis

## Audit Logging (Branch-Based)

AIDLC uses a **branch-based audit system** for team collaboration:

```
aidlc-docs/audit/
├── audit-index.md          # Master index
├── main.md                 # Main branch audit
├── feature-{name}.md       # Feature branch audits
└── archived/               # Merged branch audits
```

### How It Works
- Detects current Git branch automatically
- Creates separate audit file per branch
- Archives when branch is merged

### Logged Information
- Timestamps (ISO 8601 format)
- Current Git branch
- Complete user inputs (never summarized)
- AI actions and decisions
- Stage transitions

