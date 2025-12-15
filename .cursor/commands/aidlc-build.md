# /aidlc-build - Build and Test

Generate build and test instructions.

## What This Command Does

1. **Generate Build Instructions**
   - Prerequisites
   - Setup steps
   - Build commands
   - Troubleshooting

2. **Generate Test Instructions**
   - Unit test commands
   - Integration test commands
   - Coverage targets

3. **Create Summary**
   - Quick commands
   - Verification checklist

4. **Finalize CHANGELOG**
   - Ask for version number
   - Convert `[Unreleased]` to versioned entry
   - Add release date

## Output Files

```
aidlc-docs/branches/{branch}/construction/build-and-test/
├── build-instructions.md
├── unit-test-instructions.md
├── integration-test-instructions.md
└── build-and-test-summary.md
```

## Quick Commands

```markdown
| Action | Command |
|--------|---------|
| Build | npm run build |
| Test | npm test |
| Lint | npm run lint |
```

## Verification Checklist

- [ ] Dependencies installed
- [ ] Build successful
- [ ] Unit tests passing
- [ ] Integration tests passing
- [ ] Linting passing

## After Completion

🎉 **CONSTRUCTION PHASE COMPLETE!**

🎉 **AIDLC WORKFLOW COMPLETE!**

## Final Summary

```markdown
✅ AIDLC Workflow Complete

**Phases Completed**:
- ✅ INCEPTION
- ✅ CONSTRUCTION

**Next Steps**:
1. Execute build commands
2. Run tests
3. Deploy when ready
```

## Related Commands

- `/aidlc-status` - View final status
- `/aidlc` - Start new project

