# Project Structure Context

> **Instructions**: Fill in this file to provide project structure context for AI-assisted development.
> The AI will use this information to place new files in the correct locations and follow your patterns.

---

## Folder Layout

```
project-root/
├── src/                      # Source code
│   ├── components/           # UI components
│   │   ├── common/          # Shared components
│   │   └── features/        # Feature-specific components
│   ├── services/            # Business logic / API calls
│   ├── hooks/               # Custom React hooks
│   ├── utils/               # Utility functions
│   ├── types/               # TypeScript type definitions
│   ├── constants/           # Constants and enums
│   └── styles/              # Global styles
├── tests/                    # Test files
│   ├── unit/                # Unit tests
│   ├── integration/         # Integration tests
│   └── e2e/                 # End-to-end tests
├── public/                   # Static assets
├── docs/                     # Documentation
└── config/                   # Configuration files
```

---

## File Naming Conventions

| Type | Pattern | Example |
|------|---------|---------|
| **Components** | PascalCase | `UserProfile.tsx` |
| **Pages/Routes** | kebab-case or lowercase | `user-profile.tsx` or `userprofile.tsx` |
| **Hooks** | camelCase with `use` prefix | `useAuth.ts` |
| **Services** | camelCase or PascalCase | `userService.ts` or `UserService.ts` |
| **Utilities** | camelCase | `formatDate.ts` |
| **Types** | camelCase or PascalCase | `user.types.ts` or `UserTypes.ts` |
| **Constants** | camelCase or UPPER_CASE | `config.ts` or `CONSTANTS.ts` |
| **Tests** | Same as source + suffix | `UserProfile.test.tsx` or `UserProfile.spec.tsx` |
| **Styles** | Same as component | `UserProfile.module.css` |

---

## Module Organization

### Component Structure

```
components/
└── UserProfile/
    ├── index.ts              # Barrel export
    ├── UserProfile.tsx       # Main component
    ├── UserProfile.test.tsx  # Tests
    ├── UserProfile.module.css # Styles (if CSS modules)
    └── types.ts              # Component-specific types
```

### Service Structure

```
services/
└── user/
    ├── index.ts              # Barrel export
    ├── userService.ts        # Service implementation
    ├── userService.test.ts   # Tests
    └── types.ts              # Service-specific types
```

---

## Import Patterns

### Absolute Imports

```typescript
// Use path aliases for cleaner imports
import { Button } from '@/components/common/Button';
import { useAuth } from '@/hooks/useAuth';
import { formatDate } from '@/utils/formatDate';
```

### Import Order

```typescript
// 1. External libraries
import React from 'react';
import { useState } from 'react';

// 2. Internal absolute imports
import { Button } from '@/components/common/Button';
import { useAuth } from '@/hooks/useAuth';

// 3. Relative imports
import { UserAvatar } from './UserAvatar';
import styles from './UserProfile.module.css';

// 4. Types (can be grouped with their source)
import type { User } from '@/types/user';
```

### Barrel Exports

```typescript
// components/common/index.ts
export { Button } from './Button';
export { Input } from './Input';
export { Modal } from './Modal';
```

---

## Special Directories

| Directory | Purpose | Notes |
|-----------|---------|-------|
| `__tests__/` | Co-located tests | Alternative to `tests/` |
| `__mocks__/` | Mock files for testing | Used by Jest |
| `__fixtures__/` | Test fixtures/data | |
| `.cursor-kiro/` | Kiro-style AIDLC specs | AI workflow artifacts |

---

## Patterns to Follow

### Do

- [ ] Group related files together
- [ ] Use barrel exports (index.ts) for cleaner imports
- [ ] Keep components small and focused
- [ ] Co-locate tests with source files (or in parallel structure)
- [ ] Use meaningful, descriptive names

### Don't

- [ ] Don't create deeply nested folder structures (max 3-4 levels)
- [ ] Don't mix naming conventions
- [ ] Don't put unrelated files in the same directory
- [ ] Don't create "utils" folders that become dumping grounds

---

> **Last Updated**: [date]
> **Updated By**: [name or AI]

