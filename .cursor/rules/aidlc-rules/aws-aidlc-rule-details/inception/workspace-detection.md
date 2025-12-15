# Workspace Detection

**Purpose**: Determine workspace state and check for existing AI-DLC projects

## Step 1: Check for Existing AI-DLC Project

Detect current Git branch and check if `aidlc-docs/state/{branch}.md` exists:
- **If exists**: Resume from last phase (load context from previous phases)
- **If not exists**: Continue with new project assessment

## Step 2: Scan Workspace for Existing Code

**Determine if workspace has existing code:**
- Scan workspace for source code files (.java, .py, .js, .ts, etc.)
- Check for build files (pom.xml, package.json, build.gradle, etc.)
- Look for project structure indicators

**Record findings:**
```markdown
## Workspace State
- **Existing Code**: [Yes/No]
- **Programming Languages**: [List if found]
- **Build System**: [Maven/Gradle/npm/etc. if found]
- **Project Structure**: [Monolith/Microservices/Library/Empty]
```

## Step 3: Determine Next Phase

**IF workspace is empty (no existing code)**:
- Set flag: `brownfield = false`
- Next phase: Requirements Analysis

**IF workspace has existing code**:
- Set flag: `brownfield = true`
- Check for existing reverse engineering artifacts in `aidlc-docs/branches/{branch}/inception/reverse-engineering/`
- **IF reverse engineering artifacts exist**: Load them, skip to Requirements Analysis
- **IF no reverse engineering artifacts**: Next phase is Reverse Engineering

## Step 4: Create Initial State File

Detect current Git branch and create `aidlc-docs/state/{branch}.md`:

```markdown
# AI-DLC State: {branch-name}

## Branch Info
- **Branch**: {original-branch-name}
- **Base Branch**: {base-branch, e.g., main}
- **Created**: {ISO timestamp}
- **Current Stage**: 🔵 INCEPTION - Workspace Detection

## Project Context
- **Project Type**: [Greenfield/Brownfield]
- **Request Summary**: [Brief description of the feature/fix]

## Workspace State
- **Existing Code**: [Yes/No]
- **Reverse Engineering Needed**: [Yes/No]

## Stage Progress
[Will be populated as workflow progresses]
```

Also update `aidlc-docs/state/state-index.md` with new branch entry.

## Step 4.1: Create or Verify CHANGELOG.md

**Check if `CHANGELOG.md` exists at project root:**

- **If NOT exists**: Create from template (see `common/changelog-management.md`)
- **If exists**: Leave unchanged

**CHANGELOG Template:**

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Added
<!-- New features will be added here by AIDLC -->

### Changed
<!-- Changes to existing functionality -->

### Fixed
<!-- Bug fixes -->

### Removed
<!-- Removed features -->

---
```

**Log in branch audit file** (`aidlc-docs/audit/{branch}.md`):
- Record "CHANGELOG.md created" or "CHANGELOG.md already exists"

## Step 5: Present Completion Message

**For Brownfield Projects:**
```markdown
# 🔍 Workspace Detection Complete

Workspace analysis findings:
• **Project Type**: Brownfield project
• [AI-generated summary of workspace findings in bullet points]
• **Next Step**: Proceeding to **Reverse Engineering** to analyze existing codebase...
```

**For Greenfield Projects:**
```markdown
# 🔍 Workspace Detection Complete

Workspace analysis findings:
• **Project Type**: Greenfield project
• **Next Step**: Proceeding to **Requirements Analysis**...
```

## Step 5: Check for Multi-Repo Configuration

**Check if `aidlc-docs/related-projects.md` exists:**

- **If exists**: Load related projects configuration
- **If not exists but sibling directories detected**: Ask user if they want to configure multi-repo

**For Multi-Repo Projects:**
```markdown
📁 Related Projects Detected

I found these potential related projects:
- ../my-frontend (appears to be Frontend - React)
- ../my-backend (appears to be Backend - Node.js)
- ../my-shared (appears to be Library)

Would you like me to create a multi-repo configuration?
This helps AIDLC understand cross-project dependencies.

[Yes, configure] / [No, single project only]
```

**Log in branch audit file** (`aidlc-docs/audit/{branch}.md`):
- Record related projects if configured

---

## Step 6: Automatically Proceed

- **No user approval required** - this is informational only
- Automatically proceed to next phase:
  - **Brownfield**: Reverse Engineering (if no existing artifacts) or Requirements Analysis (if artifacts exist)
  - **Greenfield**: Requirements Analysis
