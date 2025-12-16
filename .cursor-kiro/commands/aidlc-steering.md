# /aidlc-steering - Setup Project Context

Generate or update steering files that provide context for AI-assisted development.

## What This Command Does

When you use `/aidlc-steering`, the AI will:

1. **Scan Your Codebase**
   - Analyze `package.json`, `requirements.txt`, or similar dependency files
   - Detect tech stack (languages, frameworks, libraries)
   - Analyze folder structure and naming patterns
   - Identify coding conventions from existing code

2. **Generate Steering Files**
   - `product.md` - Product vision, goals, personas (if detectable)
   - `tech.md` - Tech stack, dependencies, coding conventions
   - `structure.md` - Project structure, file naming, import patterns

3. **Ask for Review**
   - Present generated content for your review
   - Allow modifications before saving

## Prerequisites

- None (can run on any project)

## Usage

### Generate All Steering Files
```
/aidlc-steering
```

### Update Specific File
```
/aidlc-steering tech
/aidlc-steering structure
/aidlc-steering product
```

### Regenerate from Scratch
```
/aidlc-steering --regenerate
```

## Output

Files created/updated in `.cursor-kiro/steering/`:

| File | Content |
|------|---------|
| `product.md` | Product context, goals, personas |
| `tech.md` | Tech stack, conventions, API standards |
| `structure.md` | Folder structure, naming patterns |

## Example

### Input
```
/aidlc-steering
```

### AI Response
```
🔍 Scanning codebase...

📦 Detected Tech Stack:
- Language: TypeScript 5.0
- Framework: Next.js 14
- Database: PostgreSQL (via Prisma)
- Testing: Jest + React Testing Library

📁 Detected Structure:
- src/components/ - React components (PascalCase)
- src/services/ - Business logic (camelCase)
- src/utils/ - Utilities (camelCase)

📝 Generated Steering Files:

1. tech.md - Tech stack and conventions
2. structure.md - Project structure patterns

Would you like me to also generate product.md? 
(This requires manual input about your product vision)

[Review] [Save] [Modify]
```

## Tips

- Run this command **once** when starting a new project
- Update steering files when your tech stack changes
- The more complete your steering files, the better AI suggestions

## Related Commands

| Command | Description |
|---------|-------------|
| `/aidlc-requirements` | Generate requirements (uses steering context) |
| `/aidlc-design` | Generate design (uses steering context) |
| `/aidlc-task` | Generate tasks (uses steering context) |

