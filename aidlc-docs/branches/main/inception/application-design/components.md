# Components: AIDLC Command System

## Overview

AIDLC Command System ประกอบด้วย 4 กลุ่ม components หลัก:

```
┌─────────────────────────────────────────────────────────────────┐
│                    AIDLC Command System                         │
├─────────────────┬─────────────────┬─────────────────────────────┤
│   Core Layer    │  Command Layer  │      Support Layer          │
│                 │                 │                             │
│ • State Manager │ • Main Commands │ • Validation Service        │
│ • Audit Logger  │ • Inception Cmd │ • Template Service          │
│ • File Manager  │ • Construction  │ • Git Integration           │
└─────────────────┴─────────────────┴─────────────────────────────┘
```

---

## Component Group 1: Core Layer

### Component 1.1: StateManager
| Attribute | Description |
|-----------|-------------|
| **Purpose** | จัดการ state ของ AIDLC workflow |
| **Responsibilities** | - อ่าน/เขียน `aidlc-state.md`<br>- Track current stage และ phase<br>- Track completed/pending stages<br>- Resume workflow จาก last state |
| **Interface** | Cursor Rules functions |
| **Files** | `aidlc-state.md` |

### Component 1.2: AuditLogger
| Attribute | Description |
|-----------|-------------|
| **Purpose** | บันทึก audit trail ของทุก interactions |
| **Responsibilities** | - Log user inputs ด้วย timestamp<br>- Log AI actions และ decisions<br>- Append-only logging (ไม่ overwrite)<br>- Format timestamps as ISO 8601 |
| **Interface** | Cursor Rules functions |
| **Files** | `audit.md` |

### Component 1.3: FileManager
| Attribute | Description |
|-----------|-------------|
| **Purpose** | จัดการไฟล์และโฟลเดอร์ของ AIDLC |
| **Responsibilities** | - สร้าง/อ่าน/เขียน markdown files<br>- จัดการโครงสร้าง `aidlc-docs/`<br>- Validate file existence<br>- Handle file errors gracefully |
| **Interface** | Cursor Rules file operations |
| **Files** | All files in `aidlc-docs/` |

---

## Component Group 2: Command Layer

### Component 2.1: MainCommands

#### 2.1.1: AidlcCommand (`/aidlc`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Main entry point สำหรับ AIDLC workflow |
| **Responsibilities** | - Detect workspace state (greenfield/brownfield)<br>- Check for existing `aidlc-state.md`<br>- Route to appropriate next step<br>- Display welcome message |
| **Trigger** | `/aidlc` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/main.mdc` |

#### 2.1.2: InitCommand (`/aidlc-init`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Initialize AIDLC project structure |
| **Responsibilities** | - สร้าง `aidlc-docs/` directory structure<br>- สร้าง initial `aidlc-state.md`<br>- สร้าง empty `audit.md`<br>- Detect brownfield/greenfield |
| **Trigger** | `/aidlc-init` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/init.mdc` |

#### 2.1.3: StatusCommand (`/aidlc-status`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | แสดงสถานะปัจจุบันของ workflow |
| **Responsibilities** | - อ่าน `aidlc-state.md`<br>- แสดง current phase และ stage<br>- แสดง completed/pending stages<br>- แนะนำ next action |
| **Trigger** | `/aidlc-status` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/status.mdc` |

---

### Component 2.2: InceptionCommands

#### 2.2.1: ReverseCommand (`/aidlc-reverse`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Reverse engineering สำหรับ brownfield projects |
| **Responsibilities** | - Scan codebase structure<br>- Identify technologies<br>- Generate architecture docs<br>- Create component inventory |
| **Trigger** | `/aidlc-reverse` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/inception/reverse.mdc` |

#### 2.2.2: RequirementsCommand (`/aidlc-requirements`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Execute Requirements Analysis stage |
| **Responsibilities** | - Analyze user request<br>- Generate clarifying questions<br>- Create requirements.md<br>- Update state |
| **Trigger** | `/aidlc-requirements` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/inception/requirements.mdc` |

#### 2.2.3: StoriesCommand (`/aidlc-stories`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Execute User Stories stage |
| **Responsibilities** | - Assess if stories needed<br>- Generate personas<br>- Generate user stories<br>- Create stories.md และ personas.md |
| **Trigger** | `/aidlc-stories` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/inception/stories.mdc` |

#### 2.2.4: PlanCommand (`/aidlc-plan`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Execute Workflow Planning stage |
| **Responsibilities** | - Analyze requirements และ stories<br>- Determine stages to execute/skip<br>- Create execution plan<br>- Generate Mermaid diagram |
| **Trigger** | `/aidlc-plan` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/inception/plan.mdc` |

#### 2.2.5: DesignCommand (`/aidlc-design`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Execute Application Design stage |
| **Responsibilities** | - Design components<br>- Define component methods<br>- Map dependencies<br>- Create design artifacts |
| **Trigger** | `/aidlc-design` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/inception/design.mdc` |

#### 2.2.6: UnitsCommand (`/aidlc-units`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Execute Units Generation stage |
| **Responsibilities** | - Decompose system into units<br>- Define unit dependencies<br>- Map units to stories<br>- Create unit-of-work.md |
| **Trigger** | `/aidlc-units` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/inception/units.mdc` |

---

### Component 2.3: ConstructionCommands

#### 2.3.1: FunctionalCommand (`/aidlc-functional`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Execute Functional Design stage (per unit) |
| **Responsibilities** | - Design business logic<br>- Define business rules<br>- Create domain entities<br>- Generate functional design docs |
| **Trigger** | `/aidlc-functional` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/construction/functional.mdc` |

#### 2.3.2: NfrCommand (`/aidlc-nfr`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Execute NFR Requirements และ Design stages |
| **Responsibilities** | - Assess NFR requirements<br>- Recommend tech stack<br>- Design NFR patterns<br>- Create NFR documents |
| **Trigger** | `/aidlc-nfr` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/construction/nfr.mdc` |

#### 2.3.3: InfraCommand (`/aidlc-infra`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Execute Infrastructure Design stage |
| **Responsibilities** | - Map infrastructure services<br>- Define deployment architecture<br>- Specify cloud resources<br>- Generate infra docs |
| **Trigger** | `/aidlc-infra` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/construction/infra.mdc` |

#### 2.3.4: CodeCommand (`/aidlc-code`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Execute Code Generation stage (per unit) |
| **Responsibilities** | - Create code generation plan<br>- Wait for plan approval<br>- Generate code according to plan<br>- Create unit tests |
| **Trigger** | `/aidlc-code` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/construction/code.mdc` |

#### 2.3.5: BuildCommand (`/aidlc-build`)
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Execute Build and Test stage |
| **Responsibilities** | - Generate build instructions<br>- Generate test instructions<br>- Create build-and-test-summary.md |
| **Trigger** | `/aidlc-build` ใน Cursor chat |
| **File** | `.cursor/rules/aidlc-commands/construction/build.mdc` |

---

## Component Group 3: Support Layer

### Component 3.1: ValidationService
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Validate AIDLC workflow compliance |
| **Responsibilities** | - Validate stage prerequisites<br>- Validate document structure<br>- Validate Mermaid syntax<br>- Report validation errors |
| **Interface** | Internal validation functions |
| **Used By** | All command components |

### Component 3.2: TemplateService
| Attribute | Description |
|-----------|-------------|
| **Purpose** | จัดการ templates สำหรับ documents |
| **Responsibilities** | - Provide document templates<br>- Support custom templates<br>- Version template updates |
| **Interface** | Template retrieval functions |
| **Used By** | All command components |

### Component 3.3: GitIntegration
| Attribute | Description |
|-----------|-------------|
| **Purpose** | Integration กับ Git workflows |
| **Responsibilities** | - Track AIDLC artifacts<br>- Support commit on stage completion<br>- Provide PR templates |
| **Interface** | Git command wrappers |
| **Used By** | Optional for all commands |

---

## Component Summary

| Group | Count | Components |
|-------|-------|------------|
| Core Layer | 3 | StateManager, AuditLogger, FileManager |
| Main Commands | 3 | /aidlc, /aidlc-init, /aidlc-status |
| Inception Commands | 6 | /aidlc-reverse, /aidlc-requirements, /aidlc-stories, /aidlc-plan, /aidlc-design, /aidlc-units |
| Construction Commands | 5 | /aidlc-functional, /aidlc-nfr, /aidlc-infra, /aidlc-code, /aidlc-build |
| Support Layer | 3 | ValidationService, TemplateService, GitIntegration |
| **Total** | **20** | |

---

## Document History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-15 | Initial components document |

