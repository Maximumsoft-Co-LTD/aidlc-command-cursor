# /aidlc-stories - User Stories Generation

Generate user stories and personas from requirements.

## When To Use

**Execute IF:**
- New user-facing features
- User experience changes
- Multiple user personas
- Complex business requirements

**Skip IF:**
- Pure internal refactoring
- Simple bug fixes
- Infrastructure-only changes

## What This Command Does

1. **Assess Need**
   - Evaluate if user stories add value
   - Recommend skip for simple tasks

2. **Create Story Plan**
   - Generate questions about personas, granularity, format
   - Wait for user answers

3. **Generate Artifacts**
   - `personas.md` - User personas with characteristics
   - `stories.md` - User stories with acceptance criteria

## Output Files

```
aidlc-docs/branches/{branch}/inception/user-stories/
├── personas.md
└── stories.md
```

## Story Format

```markdown
### Story 1.1: {Title}

**As a** {persona}
**I want** {feature}
**So that** {benefit}

**Acceptance Criteria**:
- Given {condition}
- When {action}
- Then {result}

**Priority**: P0/P1/P2
```

## INVEST Criteria

All stories are validated:
- **I**ndependent
- **N**egotiable
- **V**aluable
- **E**stimable
- **S**mall
- **T**estable

## Related Commands

- `/aidlc-requirements` - Prerequisites
- `/aidlc-plan` - Next step

