# Component Methods: AIDLC Command System

## Overview

เอกสารนี้กำหนด method signatures สำหรับแต่ละ component  
**Note**: Detailed business rules จะถูกกำหนดใน Functional Design (CONSTRUCTION phase)

---

## Core Layer Methods

### StateManager

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `loadState()` | โหลด state จาก aidlc-state.md | - | StateObject |
| `saveState(state)` | บันทึก state ลง aidlc-state.md | StateObject | boolean |
| `getCurrentStage()` | ดึง current stage | - | StageName |
| `setCurrentStage(stage)` | ตั้ง current stage | StageName | boolean |
| `markStageComplete(stage)` | Mark stage as complete | StageName | boolean |
| `getCompletedStages()` | ดึง list ของ completed stages | - | StageName[] |
| `getPendingStages()` | ดึง list ของ pending stages | - | StageName[] |
| `isStageComplete(stage)` | เช็คว่า stage complete หรือยัง | StageName | boolean |
| `getProjectType()` | ดึง project type (greenfield/brownfield) | - | ProjectType |

### AuditLogger

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `logUserInput(input, context)` | Log user input | string, ContextObject | boolean |
| `logAIAction(action, details)` | Log AI action | string, DetailsObject | boolean |
| `logStageTransition(from, to)` | Log stage transition | StageName, StageName | boolean |
| `logApproval(stage, response)` | Log approval response | StageName, string | boolean |
| `getAuditTrail()` | ดึง audit trail ทั้งหมด | - | AuditEntry[] |
| `formatTimestamp()` | สร้าง ISO 8601 timestamp | - | string |

### FileManager

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `createDirectory(path)` | สร้าง directory | string | boolean |
| `createFile(path, content)` | สร้าง file | string, string | boolean |
| `readFile(path)` | อ่าน file content | string | string |
| `appendToFile(path, content)` | Append content to file | string, string | boolean |
| `fileExists(path)` | เช็คว่า file มีอยู่หรือไม่ | string | boolean |
| `listDirectory(path)` | List files in directory | string | string[] |
| `deleteFile(path)` | ลบ file | string | boolean |

---

## Command Layer Methods

### MainCommands

#### AidlcCommand (`/aidlc`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute()` | Main entry point | - | CommandResult |
| `detectWorkspace()` | Detect workspace state | - | WorkspaceState |
| `checkExistingState()` | Check for existing aidlc-state.md | - | boolean |
| `routeToNextStep()` | Route to appropriate step | WorkspaceState | NextStep |
| `displayWelcome()` | Display welcome message | - | void |
| `handleResume()` | Resume from existing state | StateObject | CommandResult |

#### InitCommand (`/aidlc-init`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute()` | Initialize AIDLC project | - | CommandResult |
| `createFolderStructure()` | สร้าง aidlc-docs structure | - | boolean |
| `initializeState()` | สร้าง initial aidlc-state.md | ProjectType | boolean |
| `initializeAudit()` | สร้าง initial audit.md | - | boolean |
| `detectProjectType()` | Detect greenfield/brownfield | - | ProjectType |
| `displaySuccess()` | Display success message | - | void |
| `handleError(error)` | Handle initialization errors | Error | CommandResult |

#### StatusCommand (`/aidlc-status`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute()` | Display status | - | CommandResult |
| `formatStatus()` | Format status for display | StateObject | string |
| `getProgressPercentage()` | Calculate progress percentage | StateObject | number |
| `suggestNextAction()` | Suggest next action | StateObject | string |
| `displayStatus()` | Display formatted status | - | void |

---

### InceptionCommands

#### ReverseCommand (`/aidlc-reverse`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute()` | Execute reverse engineering | - | CommandResult |
| `validatePrerequisites()` | Check if reverse engineering needed | - | boolean |
| `scanCodebase()` | Scan existing code | - | CodebaseInfo |
| `identifyTechnologies()` | Identify tech stack | CodebaseInfo | TechStack |
| `generateArchitecture()` | Generate architecture docs | CodebaseInfo | boolean |
| `createComponentInventory()` | Create component list | CodebaseInfo | boolean |
| `handleSkip()` | Handle when skipped (greenfield) | - | CommandResult |

#### RequirementsCommand (`/aidlc-requirements`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute()` | Execute requirements analysis | - | CommandResult |
| `analyzeRequest(request)` | Analyze user request | string | RequestAnalysis |
| `generateQuestions()` | Generate clarifying questions | RequestAnalysis | Question[] |
| `waitForAnswers()` | Wait for user answers | - | Answer[] |
| `createRequirementsDoc()` | Create requirements.md | Answer[] | boolean |
| `presentCompletion()` | Present completion message | - | void |

#### StoriesCommand (`/aidlc-stories`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute()` | Execute user stories generation | - | CommandResult |
| `assessNeed()` | Assess if stories needed | - | boolean |
| `generatePlan()` | Generate story plan with questions | - | StoryPlan |
| `createPersonas()` | Create personas.md | Answer[] | boolean |
| `createStories()` | Create stories.md | Answer[] | boolean |
| `validateInvestCriteria()` | Validate INVEST criteria | Story[] | boolean |

#### PlanCommand (`/aidlc-plan`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute()` | Execute workflow planning | - | CommandResult |
| `analyzeContext()` | Analyze requirements and stories | - | ContextAnalysis |
| `determineStages()` | Determine stages to execute/skip | ContextAnalysis | StageDecision[] |
| `createExecutionPlan()` | Create execution-plan.md | StageDecision[] | boolean |
| `generateMermaidDiagram()` | Generate Mermaid workflow | StageDecision[] | string |
| `validateMermaidSyntax()` | Validate Mermaid syntax | string | boolean |

#### DesignCommand (`/aidlc-design`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute()` | Execute application design | - | CommandResult |
| `identifyComponents()` | Identify system components | - | Component[] |
| `defineMethods()` | Define component methods | Component[] | Method[] |
| `mapDependencies()` | Map component dependencies | Component[] | Dependency[] |
| `createDesignArtifacts()` | Create design documents | - | boolean |

#### UnitsCommand (`/aidlc-units`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute()` | Execute units generation | - | CommandResult |
| `decomposeSystem()` | Decompose into units of work | - | Unit[] |
| `defineDependencies()` | Define unit dependencies | Unit[] | UnitDependency[] |
| `mapToStories()` | Map units to user stories | Unit[] | StoryMapping[] |
| `createUnitPlan()` | Create unit-of-work.md | Unit[] | boolean |

---

### ConstructionCommands

#### FunctionalCommand (`/aidlc-functional`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute(unitName)` | Execute functional design for unit | string | CommandResult |
| `loadUnitContext()` | Load unit context | string | UnitContext |
| `designBusinessLogic()` | Design business logic | UnitContext | BusinessLogic |
| `defineBusinessRules()` | Define business rules | UnitContext | BusinessRule[] |
| `createFunctionalDocs()` | Create functional design docs | - | boolean |

#### NfrCommand (`/aidlc-nfr`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute(unitName)` | Execute NFR stages for unit | string | CommandResult |
| `assessRequirements()` | Assess NFR requirements | - | NfrRequirement[] |
| `recommendTechStack()` | Recommend tech stack | NfrRequirement[] | TechStack |
| `designPatterns()` | Design NFR patterns | NfrRequirement[] | NfrPattern[] |
| `createNfrDocs()` | Create NFR documents | - | boolean |

#### InfraCommand (`/aidlc-infra`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute(unitName)` | Execute infrastructure design | string | CommandResult |
| `mapInfraServices()` | Map infrastructure services | - | InfraService[] |
| `defineDeployment()` | Define deployment architecture | - | DeploymentArch |
| `specifyResources()` | Specify cloud resources | - | CloudResource[] |
| `createInfraDocs()` | Create infrastructure docs | - | boolean |

#### CodeCommand (`/aidlc-code`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute(unitName)` | Execute code generation for unit | string | CommandResult |
| `loadDesignContext()` | Load design documents | string | DesignContext |
| `createCodePlan()` | Create code generation plan | DesignContext | CodePlan |
| `waitForApproval()` | Wait for plan approval | - | boolean |
| `generateCode()` | Generate code according to plan | CodePlan | CodeFiles[] |
| `generateTests()` | Generate unit tests | CodeFiles[] | TestFiles[] |
| `updateProgress()` | Update checkboxes in plan | - | boolean |

#### BuildCommand (`/aidlc-build`)

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `execute()` | Execute build and test | - | CommandResult |
| `generateBuildInstructions()` | Generate build instructions | - | boolean |
| `generateTestInstructions()` | Generate test instructions | - | boolean |
| `createSummary()` | Create build-and-test-summary.md | - | boolean |
| `validateBuild()` | Validate build success | - | boolean |

---

## Support Layer Methods

### ValidationService

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `validatePrerequisites(stage)` | Validate stage prerequisites | StageName | ValidationResult |
| `validateDocumentStructure(doc)` | Validate document structure | DocumentPath | ValidationResult |
| `validateMermaidSyntax(code)` | Validate Mermaid syntax | string | ValidationResult |
| `reportErrors(errors)` | Report validation errors | Error[] | void |

### TemplateService

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `getTemplate(name)` | Get document template | string | Template |
| `applyTemplate(template, data)` | Apply data to template | Template, object | string |
| `registerCustomTemplate(name, template)` | Register custom template | string, Template | boolean |
| `listTemplates()` | List available templates | - | string[] |

### GitIntegration

| Method | Purpose | Input | Output |
|--------|---------|-------|--------|
| `isGitInitialized()` | Check if git initialized | - | boolean |
| `stageAidlcFiles()` | Stage AIDLC files | - | boolean |
| `commitOnStageComplete(stage)` | Commit on stage completion | StageName | boolean |
| `getPRTemplate()` | Get PR template | - | string |

---

## Type Definitions

```typescript
type StageName = 
  | 'workspace-detection' | 'reverse-engineering' | 'requirements-analysis'
  | 'user-stories' | 'workflow-planning' | 'application-design' | 'units-generation'
  | 'functional-design' | 'nfr-requirements' | 'nfr-design' | 'infrastructure-design'
  | 'code-generation' | 'build-and-test';

type ProjectType = 'greenfield' | 'brownfield';

type WorkspaceState = {
  projectType: ProjectType;
  hasExistingState: boolean;
  hasExistingCode: boolean;
};

type StateObject = {
  projectType: ProjectType;
  currentStage: StageName;
  completedStages: StageName[];
  startDate: string;
};

type CommandResult = {
  success: boolean;
  message: string;
  nextAction?: string;
};
```

---

## Document History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-15 | Initial component methods document |

