# Technical Context

> **Instructions**: Fill in this file to provide technical context for AI-assisted development.
> The AI will use this information to generate code that matches your tech stack and conventions.

---

## Tech Stack

| Layer | Technology | Version | Notes |
|-------|------------|---------|-------|
| **Language** | [e.g., TypeScript] | [e.g., 5.0] | |
| **Runtime** | [e.g., Node.js] | [e.g., 20.x] | |
| **Framework** | [e.g., Next.js] | [e.g., 14.x] | |
| **Database** | [e.g., PostgreSQL] | [e.g., 15] | |
| **ORM** | [e.g., Prisma] | [e.g., 5.x] | |
| **Testing** | [e.g., Jest] | [e.g., 29.x] | |
| **Styling** | [e.g., Tailwind CSS] | [e.g., 3.x] | |

---

## Dependencies

### Production Dependencies

```json
{
  "dependency1": "^1.0.0",
  "dependency2": "^2.0.0"
}
```

### Development Dependencies

```json
{
  "dev-dependency1": "^1.0.0",
  "dev-dependency2": "^2.0.0"
}
```

---

## Coding Conventions

### General

- [ ] Use TypeScript strict mode
- [ ] Prefer functional components over class components
- [ ] Use async/await over .then() chains
- [ ] Maximum line length: [80/100/120] characters

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Variables | camelCase | `userName`, `isActive` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT` |
| Functions | camelCase | `getUserById()` |
| Classes | PascalCase | `UserService` |
| Interfaces | PascalCase (I-prefix optional) | `User` or `IUser` |
| Types | PascalCase | `UserResponse` |
| Files (components) | PascalCase | `UserProfile.tsx` |
| Files (utilities) | camelCase | `formatDate.ts` |

### Code Style

- Indentation: [spaces/tabs], size: [2/4]
- Quotes: [single/double]
- Semicolons: [yes/no]
- Trailing commas: [yes/no]

---

## API Standards

### REST API

| Aspect | Standard |
|--------|----------|
| **Base URL** | `/api/v1` |
| **Authentication** | [Bearer Token / API Key / OAuth] |
| **Request Format** | JSON |
| **Response Format** | JSON |

### Response Structure

```json
{
  "success": true,
  "data": { },
  "error": null,
  "meta": {
    "timestamp": "ISO8601",
    "requestId": "uuid"
  }
}
```

### Error Response

```json
{
  "success": false,
  "data": null,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable message",
    "details": { }
  }
}
```

### HTTP Status Codes

| Code | Usage |
|------|-------|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `DATABASE_URL` | Database connection string | Yes |
| `API_KEY` | External API key | Yes |
| `NODE_ENV` | Environment (development/production) | Yes |

---

## Testing Standards

- Unit tests: [Jest/Vitest/Mocha]
- Integration tests: [framework]
- E2E tests: [Playwright/Cypress]
- Coverage threshold: [80%/90%]

---

> **Last Updated**: [date]
> **Updated By**: [name or AI]

