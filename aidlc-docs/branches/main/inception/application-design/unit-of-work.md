# Units of Work: AIDLC Command System

## Overview

ระบบ AIDLC Command System ถูกแบ่งออกเป็น **5 Units of Work** สำหรับการพัฒนา:

```
┌─────────────────────────────────────────────────────────────────┐
│                    AIDLC Command System                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Unit 1: Core Infrastructure     Unit 2: Main Commands          │
│  ├── StateManager                ├── /aidlc                     │
│  ├── AuditLogger                 ├── /aidlc-init                │
│  └── FileManager                 └── /aidlc-status              │
│                                                                  │
│  Unit 3: Inception Commands      Unit 4: Construction Commands  │
│  ├── /aidlc-reverse              ├── /aidlc-functional          │
│  ├── /aidlc-requirements         ├── /aidlc-nfr                 │
│  ├── /aidlc-stories              ├── /aidlc-infra               │
│  ├── /aidlc-plan                 ├── /aidlc-code                │
│  ├── /aidlc-design               └── /aidlc-build               │
│  └── /aidlc-units                                               │
│                                                                  │
│  Unit 5: Support Services                                        │
│  ├── ValidationService                                          │
│  ├── TemplateService                                            │
│  ├── GitIntegration                                             │
│  └── WorkflowOrchestrator                                       │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Unit 1: Core Infrastructure

### Definition
| Attribute | Value |
|-----------|-------|
| **Name** | Core Infrastructure |
| **Type** | Foundation Module |
| **Priority** | P0 (MVP) |
| **Development Order** | 1st (Base for all other units) |

### Components
| Component | Purpose | Files |
|-----------|---------|-------|
| StateManager | จัดการ state ของ workflow | Internal logic |
| AuditLogger | บันทึก audit trail | Internal logic |
| FileManager | จัดการ files | Internal logic |

### Responsibilities
- อ่าน/เขียน `aidlc-state.md`
- อ่าน/เขียน `audit.md`
- สร้าง/อ่าน/เขียน markdown files
- Format timestamps
- Track stage progress

### Output Files
- Logic embedded in `.mdc` command files
- Shared patterns for state และ audit handling

### Estimated Effort
- **Complexity**: Low-Medium
- **LOC**: ~200 lines of rule logic

---

## Unit 2: Main Commands

### Definition
| Attribute | Value |
|-----------|-------|
| **Name** | Main Commands |
| **Type** | Command Module |
| **Priority** | P0 (MVP) |
| **Development Order** | 2nd (Depends on Core) |

### Components
| Component | Command | File |
|-----------|---------|------|
| AidlcCommand | `/aidlc` | `main.mdc` |
| InitCommand | `/aidlc-init` | `init.mdc` |
| StatusCommand | `/aidlc-status` | `status.mdc` |

### Responsibilities
- Main entry point สำหรับ workflow
- Initialize project structure
- Display current status
- Route to appropriate next step

### Output Files
```
.cursor/rules/aidlc-commands/
├── main.mdc           # /aidlc
├── init.mdc           # /aidlc-init
└── status.mdc         # /aidlc-status
```

### Estimated Effort
- **Complexity**: Medium
- **LOC**: ~300 lines total

---

## Unit 3: Inception Commands

### Definition
| Attribute | Value |
|-----------|-------|
| **Name** | Inception Commands |
| **Type** | Command Module |
| **Priority** | P0 (MVP) |
| **Development Order** | 3rd (Depends on Core + Main) |

### Components
| Component | Command | File |
|-----------|---------|------|
| ReverseCommand | `/aidlc-reverse` | `inception/reverse.mdc` |
| RequirementsCommand | `/aidlc-requirements` | `inception/requirements.mdc` |
| StoriesCommand | `/aidlc-stories` | `inception/stories.mdc` |
| PlanCommand | `/aidlc-plan` | `inception/plan.mdc` |
| DesignCommand | `/aidlc-design` | `inception/design.mdc` |
| UnitsCommand | `/aidlc-units` | `inception/units.mdc` |

### Responsibilities
- Execute INCEPTION phase stages
- Analyze requirements
- Generate user stories
- Create workflow plans
- Design application structure
- Generate units of work

### Output Files
```
.cursor/rules/aidlc-commands/inception/
├── reverse.mdc        # /aidlc-reverse
├── requirements.mdc   # /aidlc-requirements
├── stories.mdc        # /aidlc-stories
├── plan.mdc           # /aidlc-plan
├── design.mdc         # /aidlc-design
└── units.mdc          # /aidlc-units
```

### Estimated Effort
- **Complexity**: High
- **LOC**: ~600 lines total

---

## Unit 4: Construction Commands

### Definition
| Attribute | Value |
|-----------|-------|
| **Name** | Construction Commands |
| **Type** | Command Module |
| **Priority** | P0-P1 (MVP + Post-MVP) |
| **Development Order** | 4th (Depends on Inception) |

### Components
| Component | Command | File | Priority |
|-----------|---------|------|----------|
| FunctionalCommand | `/aidlc-functional` | `construction/functional.mdc` | P1 |
| NfrCommand | `/aidlc-nfr` | `construction/nfr.mdc` | P1 |
| InfraCommand | `/aidlc-infra` | `construction/infra.mdc` | P2 |
| CodeCommand | `/aidlc-code` | `construction/code.mdc` | P0 |
| BuildCommand | `/aidlc-build` | `construction/build.mdc` | P0 |

### Responsibilities
- Execute CONSTRUCTION phase stages
- Design functional logic (per unit)
- Define NFR requirements and patterns
- Design infrastructure
- Generate code
- Build and test

### Output Files
```
.cursor/rules/aidlc-commands/construction/
├── functional.mdc     # /aidlc-functional
├── nfr.mdc            # /aidlc-nfr
├── infra.mdc          # /aidlc-infra
├── code.mdc           # /aidlc-code
└── build.mdc          # /aidlc-build
```

### Estimated Effort
- **Complexity**: High
- **LOC**: ~500 lines total

---

## Unit 5: Support Services

### Definition
| Attribute | Value |
|-----------|-------|
| **Name** | Support Services |
| **Type** | Service Module |
| **Priority** | P1 (Post-MVP) |
| **Development Order** | 5th (Enhancement) |

### Components
| Component | Purpose |
|-----------|---------|
| ValidationService | Validate workflow compliance |
| TemplateService | Manage document templates |
| GitIntegration | Git workflow integration |
| WorkflowOrchestrator | Orchestrate stage transitions |

### Responsibilities
- Validate stage prerequisites
- Validate document format
- Manage templates
- Coordinate Git commits
- Orchestrate workflow

### Output Files
- Enhanced logic in existing command files
- Shared validation patterns

### Estimated Effort
- **Complexity**: Medium
- **LOC**: ~300 lines total

---

## Unit Summary

| Unit | Components | Priority | Order | Est. LOC |
|------|------------|----------|-------|----------|
| 1. Core Infrastructure | 3 | P0 | 1st | ~200 |
| 2. Main Commands | 3 | P0 | 2nd | ~300 |
| 3. Inception Commands | 6 | P0 | 3rd | ~600 |
| 4. Construction Commands | 5 | P0-P1 | 4th | ~500 |
| 5. Support Services | 4 | P1 | 5th | ~300 |
| **Total** | **21** | | | **~1900** |

---

## MVP Scope

### MVP (P0) - Must Have
| Unit | Components |
|------|------------|
| Core Infrastructure | All 3 components |
| Main Commands | All 3 commands |
| Inception Commands | All 6 commands |
| Construction Commands | `/aidlc-code`, `/aidlc-build` |

### Post-MVP (P1) - Should Have
| Unit | Components |
|------|------------|
| Construction Commands | `/aidlc-functional`, `/aidlc-nfr` |
| Support Services | All 4 components |

### Future (P2) - Nice to Have
| Unit | Components |
|------|------------|
| Construction Commands | `/aidlc-infra` |

---

## Document History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-15 | Initial unit of work document |

