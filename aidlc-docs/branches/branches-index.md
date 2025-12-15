# AIDLC Branches Index

## Overview

This directory contains branch-specific AIDLC artifacts. Each branch has its own `inception/` and `construction/` folders for parallel development.

---

## Active Branches

| Branch | Path | Status | Last Updated |
|--------|------|--------|--------------|
| main | [main/](./main/) | ✅ Complete | 2025-12-15T17:20:00Z |

## Directory Structure

```text
branches/
├── branches-index.md           # This file
├── main/
│   ├── inception/              # INCEPTION phase artifacts
│   │   ├── plans/
│   │   ├── requirements/
│   │   ├── user-stories/
│   │   ├── application-design/
│   │   └── reverse-engineering/  (brownfield only)
│   └── construction/           # CONSTRUCTION phase artifacts
│       ├── plans/
│       ├── {unit-name}/
│       └── build-and-test/
├── feature-user-auth/          # Example feature branch
│   ├── inception/
│   └── construction/
└── archived/                   # Merged branch artifacts
    └── {branch-name}/
```

---

## How It Works

### On New Branch
1. AIDLC detects new Git branch
2. Creates `branches/{sanitized-branch-name}/` directory
3. Creates `inception/` and `construction/` subdirectories
4. All artifacts for this feature go into this branch folder

### On Branch Merge
1. Move branch folder to `archived/`
2. Update branches-index.md
3. Optionally delete archived content after retention period

---

## Benefits

| Benefit | Description |
|---------|-------------|
| **Parallel Work** | Multiple features can be developed simultaneously |
| **No Conflicts** | Each branch has isolated artifacts |
| **Clear Ownership** | Easy to see who worked on what |
| **Easy Review** | PR can include all related AIDLC docs |
| **Clean History** | Main branch stays organized |

---

## Archived Branches

See `archived/` folder for completed/merged branch artifacts.

