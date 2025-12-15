# /aidlc-init - Initialize AIDLC Project

Initialize AIDLC project structure in the current workspace.

## What This Command Does

1. **Check Existing State**
   - If AIDLC already initialized → Prompt to use `/aidlc` or `--force`

2. **Detect Project Type**
   - Scan for source code files (.ts, .js, .py, .java, etc.)
   - Check for build files (package.json, pom.xml, etc.)
   - Determine: **Greenfield** or **Brownfield**

3. **Create Directory Structure**
   ```
   aidlc-docs/
   ├── inception/
   │   ├── plans/
   │   ├── requirements/
   │   ├── user-stories/
   │   ├── reverse-engineering/
   │   └── application-design/
   ├── construction/
   │   ├── plans/
   │   └── build-and-test/
   ├── branches/
   │   ├── {branch}/
   │   │   ├── inception/
   │   │   └── construction/
   ├── state/
   │   └── {branch}.md
   └── audit/
       └── {branch}.md
       ├── audit-index.md
       └── {branch}.md
   ```

4. **Create Initial Files**
   - `state/{branch}.md` - Branch-based state tracking
   - `audit/{branch}.md` - Branch-based audit trail
   - `CHANGELOG.md` - Project changelog (at project root)

## Usage

```
/aidlc-init
```

With force reinitialize:
```
/aidlc-init --force
```

## Success Output

```markdown
✅ AIDLC Initialized Successfully

**Project Type**: Greenfield/Brownfield
**Location**: aidlc-docs/

Next: Use `/aidlc` to start the workflow
```

## Related Commands

- `/aidlc` - Start/resume workflow
- `/aidlc-status` - View current status

