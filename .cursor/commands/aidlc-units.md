# /aidlc-units - Units Generation

Decompose system into units of work.

## What This Command Does

1. **Analyze Components**
   - Load application design
   - Identify logical groupings

2. **Create Units**
   - Group related functionality
   - Define unit boundaries
   - Establish development order

3. **Map Stories**
   - Assign stories to units
   - Track priority per unit

## Unit Definition

A **Unit of Work** is a logical grouping for development:
- **Microservices**: Each unit = independently deployable service
- **Monolith**: Each unit = logical module

## Output Files

```
aidlc-docs/branches/{branch}/inception/application-design/
├── unit-of-work.md
├── unit-of-work-dependency.md
└── unit-of-work-story-map.md
```

## Unit Format

```markdown
## Unit 1: {Name}

| Attribute | Value |
|-----------|-------|
| **Type** | Module/Service |
| **Priority** | P0/P1/P2 |
| **Order** | 1st/2nd/etc. |

### Components
- Component A
- Component B

### Stories
- Story 1.1
- Story 1.2
```

## After Completion

🎉 **INCEPTION PHASE COMPLETE!**

Next: Proceed to **CONSTRUCTION PHASE**

## Related Commands

- `/aidlc-functional` - Functional design
- `/aidlc-code` - Code generation

