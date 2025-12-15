# Build Instructions: AIDLC Command System

## Overview

AIDLC Command System ใช้ Cursor Custom Commands  
Files เป็น `.md` (Markdown) ที่อยู่ใน `.cursor/commands/` folder

**Reference**: [Cursor Commands Documentation](https://cursor.com/docs/agent/chat/commands)

---

## Prerequisites

| Requirement | Version | Purpose |
|-------------|---------|---------|
| **Cursor IDE** | Latest | Required to use the commands |
| **Workspace** | Any | Commands work in any workspace |

---

## Installation Steps

### Step 1: Verify File Structure

ตรวจสอบว่าไฟล์ถูกสร้างครบถ้วน:

```
.cursor/
└── commands/
    ├── aidlc.md               ✓  Main entry point
    ├── aidlc-init.md          ✓  Initialize project
    ├── aidlc-status.md        ✓  Display status
    ├── aidlc-reverse.md       ✓  Reverse engineering
    ├── aidlc-requirements.md  ✓  Requirements analysis
    ├── aidlc-stories.md       ✓  User stories
    ├── aidlc-plan.md          ✓  Workflow planning
    ├── aidlc-design.md        ✓  Application design
    ├── aidlc-units.md         ✓  Units generation
    ├── aidlc-functional.md    ✓  Functional design
    ├── aidlc-nfr.md           ✓  NFR requirements
    ├── aidlc-infra.md         ✓  Infrastructure design
    ├── aidlc-code.md          ✓  Code generation
    └── aidlc-build.md         ✓  Build and test
```

### Step 2: Verify Commands are Available

1. Open Cursor IDE
2. Open any chat window
3. Type `/` in the chat input
4. Look for `aidlc` commands in the list

### Step 3: Test Basic Command

In Cursor chat, type:
```
/aidlc
```

Expected: AI will start the AIDLC workflow with workspace detection

---

## How Commands Work

According to [Cursor documentation](https://cursor.com/docs/agent/chat/commands):

> Commands are defined as plain Markdown files that can be stored in:
> 1. **Project commands**: `.cursor/commands` directory of your project
> 2. **Global commands**: `~/.cursor/commands` directory in your home directory

When you type `/` in the chat input box, Cursor will automatically detect and display available commands.

---

## Using Parameters

You can add additional context after the command name:

```
/aidlc-requirements Build a user authentication system with OAuth2
```

Everything after the command name is included in the prompt.

---

## Verification Checklist

- [ ] All 14 `.md` files exist in `.cursor/commands/`
- [ ] Commands appear when typing `/` in chat
- [ ] `/aidlc` command responds correctly
- [ ] `/aidlc-init` creates folder structure
- [ ] `/aidlc-status` shows current state

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Commands not appearing | Verify files are in `.cursor/commands/` |
| Commands still not found | Restart Cursor IDE |
| Wrong folder | Move from `.cursor/rules/` to `.cursor/commands/` |
| File extension | Ensure files use `.md` not `.mdc` |

---

## Sharing Commands

### Project-Level (Team)
Keep commands in `.cursor/commands/` and commit to git.

### Global (Personal)
Copy to `~/.cursor/commands/` for use across all projects.

---

## Document History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-15 | Initial build instructions |
| 1.1 | 2025-12-15 | Fixed: Changed from .mdc to .md, from rules to commands |
