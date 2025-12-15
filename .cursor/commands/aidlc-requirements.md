# /aidlc-requirements - Requirements Analysis

Analyze and document project requirements.

## What This Command Does

1. **Analyze User Request**
   - Request clarity: Clear / Vague / Incomplete
   - Request type: New Feature / Bug Fix / Refactoring / etc.
   - Scope estimate: Single File → System-wide
   - Complexity: Trivial → Complex

2. **Generate Clarifying Questions**
   - Create questions document with `[Answer]:` tags
   - Wait for user to fill in answers
   - Analyze answers for ambiguities
   - Create follow-up questions if needed

3. **Generate Requirements Document**
   - Functional requirements (FR-XX)
   - Non-functional requirements (NFR-XX)
   - Success criteria
   - Assumptions and dependencies

## Output Files

```
aidlc-docs/branches/{branch}/inception/requirements/
├── requirement-verification-questions.md
└── requirements.md
```

## Usage

With a request:
```
/aidlc-requirements Build a user authentication system with OAuth
```

Without a request (will prompt):
```
/aidlc-requirements
```

## Completion

After approval, options:
- **Request Changes** - Modify requirements
- **Add User Stories** - Include user stories stage
- **Approve & Continue** - Proceed to next stage

## Related Commands

- `/aidlc-stories` - Generate user stories
- `/aidlc-plan` - Workflow planning

