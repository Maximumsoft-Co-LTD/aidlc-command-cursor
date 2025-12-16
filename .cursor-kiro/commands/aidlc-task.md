# /aidlc-task - Generate & Execute Tasks

Break down design into discrete tasks and execute them.

## What This Command Does

When you use `/aidlc-task`, the AI will:

1. **Load Context**
   - Read steering files
   - Load requirements and design for current feature

2. **Break Down Tasks**
   - Analyze design components
   - Create discrete, actionable tasks
   - Identify dependencies between tasks

3. **Sequence Tasks**
   - Order tasks by dependencies
   - Group related tasks
   - Estimate complexity

4. **Generate Checklist**
   - Create checkbox format for tracking
   - Include sub-steps for complex tasks

5. **Generate Tests**
   - Create test cases for each task
   - Include unit and integration tests

6. **Wait for Approval**
   - Present task list for review
   - Allow modifications

7. **Auto-Execute (on Approval)**
   - Execute tasks one by one
   - Update checkboxes as completed
   - Generate actual code files

## Prerequisites

- Design file must exist (run `/aidlc-design` first)
- Located at `.cursor-kiro/specs/{feature-name}/design.md`

## Usage

### Basic Usage (Generate Tasks)
```
/aidlc-task
```

### Execute Specific Task
```
/aidlc-task --execute 1
/aidlc-task --execute "Setup database schema"
```

### Execute All Tasks
```
/aidlc-task --execute-all
```

### Regenerate Tasks
```
/aidlc-task --regenerate
```

## Output

File created in `.cursor-kiro/specs/{feature-name}/tasks.md`

### Task Format

```markdown
# Tasks: [Feature Name]

## Summary
- Total Tasks: [n]
- Estimated Time: [x hours]
- Dependencies: [list]

## Task List

### Task 1: [Title]
**Status**: [ ] Pending
**Dependencies**: None
**Estimated**: 30 min
**Files**:
- [ ] `src/services/authService.ts`
- [ ] `src/services/authService.test.ts`

**Steps**:
1. [ ] Create AuthService class
2. [ ] Implement login method
3. [ ] Implement register method
4. [ ] Add unit tests

### Task 2: [Title]
**Status**: [ ] Pending
**Dependencies**: Task 1
...

## Tests

### Unit Tests
- [ ] AuthService.login() - valid credentials
- [ ] AuthService.login() - invalid credentials
- [ ] AuthService.register() - new user

### Integration Tests
- [ ] POST /api/auth/login - success flow
- [ ] POST /api/auth/register - success flow
```

## Example

### Input
```
/aidlc-task
```

### AI Response
```
📋 Generating Tasks...

🔍 Loading:
- Design: user-auth
- Components: 4
- API Endpoints: 4

---

# Tasks: User Authentication

## Summary
| Metric | Value |
|--------|-------|
| Total Tasks | 6 |
| Estimated | 4 hours |
| Test Coverage | 12 tests |

## Task List

### Task 1: Setup Database Schema
**Status**: [ ] Pending
**Dependencies**: None
**Estimated**: 15 min

**Files**:
- [ ] `prisma/schema.prisma` (update)
- [ ] `prisma/migrations/` (generate)

**Steps**:
1. [ ] Add User model to schema
2. [ ] Add PasswordResetToken model
3. [ ] Run migration

---

### Task 2: Create AuthService
**Status**: [ ] Pending
**Dependencies**: Task 1
**Estimated**: 45 min

**Files**:
- [ ] `src/services/auth/authService.ts`
- [ ] `src/services/auth/authService.test.ts`
- [ ] `src/services/auth/types.ts`

**Steps**:
1. [ ] Create AuthService class
2. [ ] Implement hashPassword()
3. [ ] Implement verifyPassword()
4. [ ] Implement generateToken()
5. [ ] Add unit tests

---

### Task 3: Create API Routes
**Status**: [ ] Pending
**Dependencies**: Task 2
**Estimated**: 1 hour

**Files**:
- [ ] `src/app/api/auth/register/route.ts`
- [ ] `src/app/api/auth/login/route.ts`
- [ ] `src/app/api/auth/forgot-password/route.ts`
- [ ] `src/app/api/auth/reset-password/route.ts`

---

[Approve & Execute All] [Execute One by One] [Modify]
```

### After Execution

```
✅ Task 1: Setup Database Schema - COMPLETED
   - Created User model
   - Created PasswordResetToken model
   - Migration applied: 20241216_add_auth_models

✅ Task 2: Create AuthService - COMPLETED
   - Created src/services/auth/authService.ts
   - Created src/services/auth/authService.test.ts
   - All 6 tests passing

🔄 Task 3: Create API Routes - IN PROGRESS
   - Created /api/auth/register
   - Creating /api/auth/login...
```

## Tips

- Review tasks before executing
- Execute one by one for complex features
- Check generated tests after each task
- Commit after each completed task

## Related Commands

| Command | Description |
|---------|-------------|
| `/aidlc-steering` | Setup project context |
| `/aidlc-requirements` | Generate requirements |
| `/aidlc-design` | Generate design |

