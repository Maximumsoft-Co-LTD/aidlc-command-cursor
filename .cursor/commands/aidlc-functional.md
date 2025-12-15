# /aidlc-functional - Functional Design

Design detailed business logic per unit.

## What This Command Does

1. **Load Unit Context**
   - Unit definition
   - Assigned stories
   - Component structure

2. **Design Business Logic**
   - Pseudocode for functions
   - Algorithm descriptions
   - Data transformations

3. **Define Business Rules**
   - Rule conditions
   - Rule actions
   - Enforcement methods

4. **Document Domain Entities**
   - Entity definitions
   - Relationships
   - Type structures

## Output Files

```
aidlc-docs/branches/{branch}/construction/{unit-name}/functional-design/
├── business-logic-model.md
├── business-rules.md
└── domain-entities.md
```

## Usage

For current unit:
```
/aidlc-functional
```

For specific unit:
```
/aidlc-functional unit-1-core
```

## Business Logic Format

```markdown
### BL-{ID}: {Function Name}

FUNCTION functionName(params):
    IF condition:
        action
    RETURN result
```

## Business Rules Format

```markdown
### BR-{ID}: {Rule Name}

RULE: RULE_NAME
    condition: When this applies
    action: What must happen
    enforcement: How it's enforced
```

## Related Commands

- `/aidlc-nfr` - NFR requirements
- `/aidlc-code` - Code generation

