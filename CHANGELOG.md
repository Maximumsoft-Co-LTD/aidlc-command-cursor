# Changelog

All notable changes to AIDLC Command System will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Planned
- Operations phase implementation (deploy, monitor)
- Additional code generation templates
- Integration with CI/CD pipelines

---

## [1.4.0] - 2025-12-15

### Added
- **Multi-Repository Support**: AIDLC can now understand context from related repos
  - New command: `/aidlc-multi-repo` - Configure multi-repo projects
  - New rule: `common/multi-repo-context.md` - Multi-repo management guide
  - Updated `workspace-detection.md` to detect related projects
  - Support for Frontend + Backend + Jobs separation
  - Cross-project impact analysis
  - Integration point documentation
  - Cursor multi-root workspace integration

---

## [1.3.0] - 2025-12-15

### Changed
- **Branch-Based Audit Consistency**: Updated all rules and commands to use branch-based audit system
  - Updated 7 INCEPTION rules (workspace-detection, reverse-engineering, requirements-analysis, user-stories, workflow-planning, application-design, units-generation)
  - Updated 6 CONSTRUCTION rules (functional-design, nfr-requirements, nfr-design, infrastructure-design, code-generation, build-and-test)
  - Updated 6 COMMON rules (changelog-management, workflow-changes, terminology, session-continuity, error-handling, depth-levels)
  - Updated 3 Commands (aidlc-init, aidlc, README)
  - Updated core-workflow.mdc for consistency
  - All references now point to `aidlc-docs/audit/{branch}.md` instead of `audit.md`

---

## [1.2.0] - 2025-12-15

### Added
- **CHANGELOG Management**: Automatic CHANGELOG.md creation and updates in user projects
  - Creates CHANGELOG.md during project initialization (aidlc-init)
  - Updates CHANGELOG after each unit's code generation
  - Finalizes version during Build and Test stage
  - Follows [Keep a Changelog](https://keepachangelog.com) format
  - New rule file: `common/changelog-management.md`

### Changed
- **workspace-detection.md**: Added CHANGELOG.md creation step
- **code-generation.md**: Added Step 12.1 for CHANGELOG updates
- **build-and-test.md**: Added Step 8 for CHANGELOG version finalization
- **aidlc-init.md**: Updated to mention CHANGELOG creation
- **aidlc-code.md**: Added CHANGELOG update to workflow
- **aidlc-build.md**: Added CHANGELOG finalization to workflow

---

## [1.1.0] - 2025-12-15

### Added
- **Helper Scripts** - New `scripts/` folder with installation utilities
  - `install-global.sh` - Install AIDLC globally for all projects
  - `install-to-project.sh` - Install AIDLC to a specific project
  - `prepare-distribution.sh` - Prepare repo for team distribution
- **Distribution Guide** - New `DISTRIBUTION.md` with team sharing instructions
- **Team Collaboration Section** - Added to README with branch-based audit explanation
- **Troubleshooting Section** - Added to README with common issues and solutions
- **.gitignore** - Ignore generated artifacts in template repo

### Changed
- **README.md** - Major rewrite with improved structure
  - Better installation instructions (3 options + scripts)
  - Clearer command tables with descriptions
  - Updated project structure diagram
  - Added version history

### Fixed
- Badge count now correctly shows 14 commands

---

## [1.0.0] - 2025-12-15

### Added
- **Initial Release** of AIDLC Command System

#### Commands (14 total)
- `/aidlc` - Main entry point, start or resume workflow
- `/aidlc-init` - Initialize project structure
- `/aidlc-status` - Show current workflow status

#### INCEPTION Phase Commands
- `/aidlc-reverse` - Reverse engineering for brownfield projects
- `/aidlc-requirements` - Requirements analysis
- `/aidlc-stories` - User stories generation
- `/aidlc-plan` - Workflow planning
- `/aidlc-design` - Application design
- `/aidlc-units` - Units of work generation

#### CONSTRUCTION Phase Commands
- `/aidlc-functional` - Functional design
- `/aidlc-nfr` - Non-functional requirements & design
- `/aidlc-infra` - Infrastructure design
- `/aidlc-code` - Code generation
- `/aidlc-build` - Build & test instructions

#### Rules System
- Core workflow rules (`core-workflow.mdc`)
- INCEPTION phase rules (7 files)
- CONSTRUCTION phase rules (6 files)
- Common utilities (10 files)

#### Features
- **Greenfield/Brownfield Detection** - Auto-detect project type
- **Adaptive Depth** - Minimal/Standard/Comprehensive execution levels
- **Branch-Based Audit System** - Separate audit logs per Git branch
- **Resume Capability** - Continue from last stage via `aidlc-state.md`
- **Checkpoint System** - User approval at each stage transition

---

## Version Numbering

| Version Type | When to Use | Example |
|--------------|-------------|---------|
| **Major** (X.0.0) | Breaking changes, workflow restructure | 2.0.0 |
| **Minor** (1.X.0) | New features, new commands | 1.2.0 |
| **Patch** (1.0.X) | Bug fixes, documentation updates | 1.0.1 |

---

## Links

- [README](README.md)
- [Distribution Guide](DISTRIBUTION.md)
- [Commands Documentation](.cursor/commands/README.md)

