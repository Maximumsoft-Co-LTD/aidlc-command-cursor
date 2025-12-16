# /aidlc-requirements - Generate Requirements

Transform natural language feature descriptions into structured requirements with acceptance criteria.

## What This Command Does

When you use `/aidlc-requirements`, the AI will:

1. **Load Context**
   - Read steering files (product.md, tech.md, structure.md)
   - Understand your project's context

2. **Parse Your Request**
   - Analyze your natural language description
   - Identify functional requirements
   - Identify non-functional requirements

3. **Generate EARS Requirements**
   - Use EARS notation (Easy Approach to Requirements Syntax)
   - WHEN [trigger] THEN system SHALL [behavior]
   - Create clear, testable requirements

4. **Generate Acceptance Criteria**
   - Define success criteria for each requirement
   - Create checkable items

5. **Clarify if Needed**
   - Ask questions if requirements are ambiguous
   - Suggest alternatives or considerations

6. **Wait for Approval**
   - Present requirements for review
   - Allow modifications before saving

## Prerequisites

- Steering files (recommended but not required)
- Run `/aidlc-steering` first for best results

## Usage

### Basic Usage
```
/aidlc-requirements สร้าง user authentication system
```

### With Feature Name
```
/aidlc-requirements --name user-auth สร้าง login/register system
```

### Continue Existing Feature
```
/aidlc-requirements --continue user-auth
```

## Output

File created in `.cursor-kiro/specs/{feature-name}/requirements.md`

### Requirements Format

```markdown
# Requirements: [Feature Name]

## Overview
[Brief description of the feature]

## Functional Requirements

### FR-001: [Title]
**WHEN** [trigger condition]
**THEN** system SHALL [expected behavior]

### FR-002: [Title]
**WHEN** [trigger condition]
**AND** [additional condition]
**THEN** system SHALL [expected behavior]

## Non-Functional Requirements

### NFR-001: [Title]
**THE** system SHALL [constraint/quality attribute]

## Acceptance Criteria

- [ ] AC-001: [criterion]
- [ ] AC-002: [criterion]
- [ ] AC-003: [criterion]
```

## Example

### Input
```
/aidlc-requirements สร้าง user authentication พร้อม login, register, และ forgot password
```

### AI Response
```
📋 Generating Requirements...

🔍 Context Loaded:
- Tech: Next.js + TypeScript + Prisma
- Auth: JWT-based (from tech.md)

---

# Requirements: User Authentication

## Overview
User authentication system with login, registration, and password recovery.

## Functional Requirements

### FR-001: User Registration
**WHEN** a visitor submits registration form with email and password
**THEN** system SHALL create a new user account
**AND** send verification email

### FR-002: User Login
**WHEN** a user submits valid credentials
**THEN** system SHALL authenticate the user
**AND** return JWT access token

### FR-003: Forgot Password
**WHEN** a user requests password reset
**THEN** system SHALL send reset link to registered email

## Acceptance Criteria

- [ ] AC-001: User can register with email/password
- [ ] AC-002: User receives verification email
- [ ] AC-003: User can login with valid credentials
- [ ] AC-004: User receives JWT token on successful login
- [ ] AC-005: User can request password reset
- [ ] AC-006: Password reset link expires after 24 hours

---

❓ Clarifying Questions:
1. Should we support social login (Google, GitHub)?
2. What's the password policy (min length, complexity)?

[Approve] [Modify] [Answer Questions]
```

## EARS Notation Reference

| Pattern | Template | Example |
|---------|----------|---------|
| **Ubiquitous** | THE system SHALL [action] | THE system SHALL log all errors |
| **Event-Driven** | WHEN [trigger] THEN [action] | WHEN user clicks submit THEN validate form |
| **State-Driven** | WHILE [state] THE system SHALL [action] | WHILE offline THE system SHALL queue requests |
| **Optional** | WHERE [condition] THE system SHALL [action] | WHERE user is admin THE system SHALL show dashboard |
| **Complex** | WHEN [trigger] AND [condition] THEN [action] | WHEN timer expires AND user inactive THEN logout |

## Related Commands

| Command | Description |
|---------|-------------|
| `/aidlc-steering` | Setup project context |
| `/aidlc-design` | Generate design from requirements |
| `/aidlc-task` | Generate tasks from design |

