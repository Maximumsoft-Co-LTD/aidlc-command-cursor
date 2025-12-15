# /aidlc-reverse - Reverse Engineering

Analyze existing codebase for brownfield projects.

## When To Use

- **Brownfield projects only** (existing code)
- For greenfield projects, this will be skipped

## What This Command Does

1. **Scan Codebase**
   - Identify programming languages
   - Detect frameworks and libraries
   - Map project structure

2. **Generate Documentation**
   - `architecture.md` - System architecture overview
   - `component-inventory.md` - List of components
   - `technology-stack.md` - Technologies used
   - `dependencies.md` - External dependencies

3. **Output Location**
   ```
   aidlc-docs/branches/{branch}/inception/reverse-engineering/
   ├── architecture.md
   ├── component-inventory.md
   ├── technology-stack.md
   └── dependencies.md
   ```

## Usage

```
/aidlc-reverse
```

## For Greenfield Projects

If this is a greenfield (new) project:
```markdown
ℹ️ Reverse Engineering Not Needed

This is a greenfield project with no existing code.

Next: Use `/aidlc-requirements` to proceed.
```

## Related Commands

- `/aidlc-requirements` - Next step after reverse engineering
- `/aidlc-status` - View current progress

