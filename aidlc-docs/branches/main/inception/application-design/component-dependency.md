# Component Dependencies: AIDLC Command System

## Overview

เอกสารนี้แสดง dependency relationships และ communication patterns ระหว่าง components

---

## Dependency Matrix

### Core Layer Dependencies

| Component | Depends On | Used By |
|-----------|------------|---------|
| **StateManager** | FileManager | All Commands, WorkflowOrchestrator |
| **AuditLogger** | FileManager | All Commands, WorkflowOrchestrator |
| **FileManager** | - (Base) | StateManager, AuditLogger, DocumentGenerator |

### Command Layer Dependencies

| Component | Depends On | Uses |
|-----------|------------|------|
| **AidlcCommand** | StateManager, AuditLogger, FileManager | WorkflowOrchestrator |
| **InitCommand** | FileManager, StateManager, AuditLogger | - |
| **StatusCommand** | StateManager | - |
| **ReverseCommand** | StateManager, AuditLogger, FileManager | DocumentGenerator |
| **RequirementsCommand** | StateManager, AuditLogger, FileManager | DocumentGenerator |
| **StoriesCommand** | StateManager, AuditLogger, FileManager | DocumentGenerator |
| **PlanCommand** | StateManager, AuditLogger, FileManager | DocumentGenerator, ValidationService |
| **DesignCommand** | StateManager, AuditLogger, FileManager | DocumentGenerator |
| **UnitsCommand** | StateManager, AuditLogger, FileManager | DocumentGenerator |
| **FunctionalCommand** | StateManager, AuditLogger, FileManager | DocumentGenerator |
| **NfrCommand** | StateManager, AuditLogger, FileManager | DocumentGenerator |
| **InfraCommand** | StateManager, AuditLogger, FileManager | DocumentGenerator |
| **CodeCommand** | StateManager, AuditLogger, FileManager | DocumentGenerator, IntegrationCoordinator |
| **BuildCommand** | StateManager, AuditLogger, FileManager | DocumentGenerator |

### Service Layer Dependencies

| Component | Depends On | Used By |
|-----------|------------|---------|
| **WorkflowOrchestrator** | StateManager, AuditLogger, ValidationService, IntegrationCoordinator | All Commands |
| **DocumentGenerator** | FileManager, TemplateService, ValidationService | All Commands |
| **IntegrationCoordinator** | FileManager, GitIntegration | CodeCommand, WorkflowOrchestrator |

### Support Layer Dependencies

| Component | Depends On | Used By |
|-----------|------------|---------|
| **ValidationService** | - | WorkflowOrchestrator, DocumentGenerator, PlanCommand |
| **TemplateService** | - | DocumentGenerator |
| **GitIntegration** | - | IntegrationCoordinator |

---

## Dependency Graph

```mermaid
graph TD
    subgraph CoreLayer["Core Layer"]
        FM[FileManager]
        SM[StateManager]
        AL[AuditLogger]
    end
    
    subgraph ServiceLayer["Service Layer"]
        WO[WorkflowOrchestrator]
        DG[DocumentGenerator]
        IC[IntegrationCoordinator]
    end
    
    subgraph SupportLayer["Support Layer"]
        VS[ValidationService]
        TS[TemplateService]
        GI[GitIntegration]
    end
    
    subgraph CommandLayer["Command Layer"]
        MC[Main Commands]
        INC[Inception Commands]
        CONC[Construction Commands]
    end
    
    %% Core Dependencies
    SM --> FM
    AL --> FM
    
    %% Service Dependencies
    WO --> SM
    WO --> AL
    WO --> VS
    WO --> IC
    DG --> FM
    DG --> TS
    DG --> VS
    IC --> FM
    IC --> GI
    
    %% Command Dependencies
    MC --> SM
    MC --> AL
    MC --> WO
    INC --> SM
    INC --> AL
    INC --> DG
    CONC --> SM
    CONC --> AL
    CONC --> DG
    CONC --> IC
    
    style FM fill:#E3F2FD,stroke:#1565C0
    style SM fill:#E3F2FD,stroke:#1565C0
    style AL fill:#E3F2FD,stroke:#1565C0
    style WO fill:#E8F5E9,stroke:#2E7D32
    style DG fill:#E8F5E9,stroke:#2E7D32
    style IC fill:#E8F5E9,stroke:#2E7D32
    style VS fill:#FFF3E0,stroke:#E65100
    style TS fill:#FFF3E0,stroke:#E65100
    style GI fill:#FFF3E0,stroke:#E65100
    style MC fill:#F3E5F5,stroke:#7B1FA2
    style INC fill:#F3E5F5,stroke:#7B1FA2
    style CONC fill:#F3E5F5,stroke:#7B1FA2
```

---

## Communication Patterns

### Pattern 1: Command Execution Flow

```mermaid
sequenceDiagram
    participant User
    participant Cmd as Command
    participant WO as WorkflowOrchestrator
    participant SM as StateManager
    participant AL as AuditLogger
    participant DG as DocumentGenerator

    User->>Cmd: /aidlc-{command}
    Cmd->>WO: requestExecution()
    WO->>SM: loadState()
    SM-->>WO: currentState
    WO->>AL: logStart()
    WO->>Cmd: execute()
    Cmd->>DG: generateDocs()
    DG-->>Cmd: success
    Cmd-->>WO: result
    WO->>SM: updateState()
    WO->>AL: logComplete()
    WO-->>User: displayResult()
```

### Pattern 2: State Management Flow

```mermaid
sequenceDiagram
    participant Cmd as Command
    participant SM as StateManager
    participant FM as FileManager
    participant AL as AuditLogger

    Cmd->>SM: loadState()
    SM->>FM: readFile(aidlc-state.md)
    FM-->>SM: fileContent
    SM-->>Cmd: StateObject
    
    Note over Cmd: Execute logic
    
    Cmd->>SM: saveState(newState)
    SM->>FM: writeFile(aidlc-state.md, content)
    FM-->>SM: success
    Cmd->>AL: logTransition()
```

### Pattern 3: Document Generation Flow

```mermaid
sequenceDiagram
    participant Cmd as Command
    participant DG as DocumentGenerator
    participant TS as TemplateService
    participant VS as ValidationService
    participant FM as FileManager

    Cmd->>DG: generateDocument(type, data)
    DG->>TS: getTemplate(type)
    TS-->>DG: template
    DG->>DG: applyTemplate(template, data)
    DG->>VS: validateFormat(content)
    VS-->>DG: validationResult
    alt Valid
        DG->>FM: createFile(path, content)
        FM-->>DG: success
    else Invalid
        DG-->>Cmd: validationError
    end
    DG-->>Cmd: result
```

---

## Data Flow Diagram

```mermaid
flowchart LR
    subgraph Input["Input"]
        UI[User Input]
        EX[Existing State]
        ER[Existing Rules]
    end
    
    subgraph Processing["Processing"]
        CMD[Commands]
        SVC[Services]
    end
    
    subgraph Storage["Storage"]
        ST[aidlc-state.md]
        AU[audit.md]
        DOC[Documents]
        RUL[Rule Files]
    end
    
    subgraph Output["Output"]
        MSG[Messages]
        ART[Artifacts]
    end
    
    UI --> CMD
    EX --> CMD
    ER --> SVC
    CMD --> SVC
    SVC --> ST
    SVC --> AU
    SVC --> DOC
    CMD --> RUL
    CMD --> MSG
    SVC --> ART
```

---

## Circular Dependency Prevention

### Rules
1. **Core Layer**: ไม่ depend on Service หรือ Command layers
2. **Service Layer**: Depend on Core, Support เท่านั้น
3. **Command Layer**: Depend on Core, Service, Support
4. **Support Layer**: ไม่ depend on ใครเลย (Base utilities)

### Dependency Direction
```
Support Layer ← Core Layer ← Service Layer ← Command Layer
```

---

## Component Initialization Order

```mermaid
graph LR
    A[1. FileManager] --> B[2. StateManager]
    A --> C[3. AuditLogger]
    B --> D[4. ValidationService]
    E[5. TemplateService] --> F[6. DocumentGenerator]
    G[7. GitIntegration] --> H[8. IntegrationCoordinator]
    D --> I[9. WorkflowOrchestrator]
    F --> I
    H --> I
    I --> J[10. Commands]
```

### Initialization Sequence
1. **FileManager** - Base file operations
2. **StateManager** - Depends on FileManager
3. **AuditLogger** - Depends on FileManager
4. **ValidationService** - Standalone
5. **TemplateService** - Standalone
6. **DocumentGenerator** - Depends on FileManager, TemplateService
7. **GitIntegration** - Standalone (optional)
8. **IntegrationCoordinator** - Depends on FileManager, GitIntegration
9. **WorkflowOrchestrator** - Depends on StateManager, ValidationService, IntegrationCoordinator
10. **Commands** - Depends on all services

---

## Error Propagation

### Error Flow
```
Component Error → Service Layer → WorkflowOrchestrator → Command → User
                       ↓
                 AuditLogger (log error)
```

### Error Handling Responsibilities

| Layer | Responsibility |
|-------|---------------|
| **Core** | Throw specific errors (FileNotFound, StateCorrupt) |
| **Service** | Catch, log, rethrow with context |
| **Command** | Catch, format user-friendly message |
| **User** | See formatted error with suggested action |

---

## Document History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-15 | Initial component dependency document |

