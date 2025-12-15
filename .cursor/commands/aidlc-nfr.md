# /aidlc-nfr - NFR Requirements & Design

Define non-functional requirements and design patterns.

## When To Use

**Execute IF:**
- Performance requirements exist
- Security considerations needed
- Scalability concerns present
- Tech stack selection required

**Skip IF:**
- Simple project
- No NFR concerns
- Tech stack already determined

## What This Command Does

1. **Assess NFR Requirements**
   - Performance targets
   - Security needs
   - Scalability goals
   - Usability requirements

2. **Make Tech Stack Decisions**
   - Language selection
   - Framework selection
   - Database selection
   - Rationale for choices

3. **Design NFR Patterns**
   - Performance patterns
   - Security patterns
   - Error handling patterns

## Output Files

```
aidlc-docs/branches/{branch}/construction/{unit-name}/nfr-requirements/
├── nfr-requirements.md
└── tech-stack-decisions.md

aidlc-docs/branches/{branch}/construction/{unit-name}/nfr-design/
└── nfr-design-patterns.md
```

## NFR Format

```markdown
### NFR-PERF-01: {Requirement}

- **Target**: Response time < 200ms
- **Measurement**: API latency monitoring
- **Priority**: P0
```

## Related Commands

- `/aidlc-infra` - Infrastructure design
- `/aidlc-code` - Code generation

