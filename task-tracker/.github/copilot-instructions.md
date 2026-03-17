# Copilot Repository Instructions

You are working in a TypeScript monorepo for a Task Tracker application.

## Tech Stack

- **Frontend**: Angular 17+ with standalone components
- **Backend**: Node.js with Express
- **Database**: MongoDB with Mongoose
- **Shared**: TypeScript types and Zod validators
- **Testing**: Jest (backend), Jasmine/Karma (frontend)

## Product Purpose

This app helps users create, update, filter, and complete personal tasks.

## Repository Structure

```
task-tracker/
├── apps/
│   ├── web/           # Angular frontend
│   └── api/           # Express backend
├── packages/
│   └── shared/        # Shared types & validators
├── docs/              # Documentation
└── .github/           # Copilot instructions & prompts
```

## Engineering Standards

- Prefer TypeScript with strict typing.
- Do not use `any` unless explicitly justified in a comment.
- Keep functions small and focused.
- Prefer pure functions for business logic.
- Favor composition over inheritance.
- Keep UI components presentational when possible.
- Put business rules in services, not in route handlers or Angular components.
- Use RxJS observables for async operations in Angular.
- Use async/await for async operations in Node.js.

## Architecture Rules

- Frontend must not define duplicate domain types that already exist in `packages/shared`.
- API routes should validate input before invoking services.
- Services should contain business logic.
- Shared validators and types belong in `packages/shared`.
- Do not access persistence logic directly from UI code.
- Use Mongoose models for database operations.
- Keep Angular components focused on presentation; delegate logic to services.

## Quality Rules

- Add or update tests for all behavior changes.
- Preserve backward compatibility unless the task explicitly allows breaking changes.
- If you change an API contract, update `docs/api-contract.md`.
- If you add a feature, verify acceptance criteria in `docs/product-spec.md`.
- Prefer accessible UI patterns with labels, keyboard support, and semantic HTML.
- Use Angular reactive forms for form handling.

## Safety Rules

- Never hardcode secrets.
- Do not invent environment variables; use documented ones only.
- Do not invent libraries or project files that do not exist.
- If uncertain, propose the smallest safe change and explain assumptions.
- Sanitize user input before database operations.
- Use environment variables for configuration.

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| MONGODB_URI | MongoDB connection string | mongodb://localhost:27017/task-tracker |
| PORT | API server port | 3000 |
| NODE_ENV | Environment mode | development |
| CORS_ORIGIN | Allowed CORS origin | http://localhost:4200 |

## Validation Checklist

Before finalizing changes:
1. Run type-check: `npm run typecheck`
2. Run lint: `npm run lint`
3. Run tests: `npm run test`
4. Summarize changed files.
5. Note any assumptions or follow-ups.
