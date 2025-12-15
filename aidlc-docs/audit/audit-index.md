# AIDLC Audit Index

Master index for all branch-based audit trails.

---

## Active Branches

| Branch | Audit File | Last Updated | Status |
|--------|------------|--------------|--------|
| main | [main.md](./main.md) | 2025-12-15 | ✅ Complete (Initial Dev) |
| refactor/command | [refactor-command.md](./refactor-command.md) | 2025-12-15 | ✅ Complete |

---

## Recently Merged

| Branch | Merged To | Merge Date | PR/MR |
|--------|-----------|------------|-------|
| *(none yet)* | - | - | - |

---

## Archived

See `archived/` folder for completed branch audits.

---

## How Branch-Based Audit Works

### When Starting Work on a New Branch

1. AIDLC detects the current Git branch
2. Creates `audit/{branch-name}.md` if it doesn't exist
3. All interactions are logged to that branch's audit file

### Branch Name Sanitization

| Git Branch | Audit File |
|------------|------------|
| `main` | `main.md` |
| `feature/user-auth` | `feature-user-auth.md` |
| `bugfix/login-fix` | `bugfix-login-fix.md` |
| `feature/REQ-001-payment` | `feature-req-001-payment.md` |

### After Merging

1. Move audit file to `archived/` folder
2. Add summary to target branch (e.g., main.md)
3. Update this index

---

## Quick Stats

- **Total Active Branches**: 2
- **Total Archived Branches**: 0
- **Last Updated**: 2025-12-15T17:55:00Z

