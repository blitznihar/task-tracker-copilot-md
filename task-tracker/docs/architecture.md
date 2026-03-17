# Architecture

## Overview

Task Tracker is a TypeScript monorepo with three main packages:

| Package | Technology | Purpose |
|---------|------------|---------|
| `apps/web` | Angular 17+ | Frontend UI |
| `apps/api` | Express + MongoDB | Backend API |
| `packages/shared` | TypeScript | Shared types and validators |

## System Diagram

```
┌─────────────────┐     HTTP/JSON     ┌─────────────────┐     Mongoose     ┌─────────────────┐
│                 │ ───────────────▶  │                 │ ───────────────▶ │                 │
│   Angular App   │                   │   Express API   │                  │    MongoDB      │
│   (apps/web)    │ ◀───────────────  │   (apps/api)    │ ◀─────────────── │                 │
│   Port 4200     │                   │   Port 3000     │                  │   Port 27017    │
└─────────────────┘                   └─────────────────┘                  └─────────────────┘
         │                                    │
         └────────────────┬───────────────────┘
                          ▼
              ┌───────────────────────┐
              │   packages/shared     │
              │  (Types, Validators)  │
              └───────────────────────┘
```

## Frontend Architecture (Angular)

### Layers

```
┌─────────────────────────────────────────┐
│            Pages (Routes)               │  Route-level smart components
├─────────────────────────────────────────┤
│            Components                   │  Reusable presentational components
├─────────────────────────────────────────┤
│            Services                     │  API calls, state management
├─────────────────────────────────────────┤
│            Shared Types                 │  From packages/shared
└─────────────────────────────────────────┘
```

### Key Decisions

- **Standalone components** — No NgModules, all components are standalone
- **OnPush change detection** — For performance
- **Reactive forms** — For form handling
- **RxJS** — For async operations
- **SCSS** — For component styles

### File Structure

```
apps/web/src/app/
├── components/
│   ├── task-form/
│   ├── task-list/
│   ├── task-item/
│   └── task-filter/
├── pages/
│   └── home/
├── services/
│   └── task.service.ts
└── app.component.ts
```

## Backend Architecture (Express)

### Layers

```
┌─────────────────────────────────────────┐
│            Routes                       │  HTTP handling, validation
├─────────────────────────────────────────┤
│            Services                     │  Business logic
├─────────────────────────────────────────┤
│            Models                       │  Mongoose schemas
├─────────────────────────────────────────┤
│            Middleware                   │  Error handling, logging
└─────────────────────────────────────────┘
```

### Key Decisions

- **Thin routes** — Routes only handle HTTP concerns
- **Service layer** — All business logic lives here
- **Zod validation** — Request validation before service calls
- **Mongoose** — MongoDB ODM with schema validation
- **Consistent responses** — Standard `{ success, data/error }` format

### File Structure

```
apps/api/src/
├── routes/
│   └── tasks.routes.ts
├── services/
│   └── task.service.ts
├── models/
│   └── task.model.ts
├── middleware/
│   ├── error.middleware.ts
│   └── validation.middleware.ts
├── config/
│   └── database.ts
└── index.ts
```

## Shared Package

### Purpose

Single source of truth for:
- Domain types (Task, CreateTaskInput, etc.)
- Validation schemas (Zod)
- Constants (priorities, statuses)

### Structure

```
packages/shared/src/
├── types.ts       # TypeScript interfaces
├── validators.ts  # Zod schemas
└── index.ts       # Exports
```

## Data Flow

### Create Task Flow

```
1. User fills form         → TaskFormComponent
2. Form validated          → Reactive form validators
3. Submit clicked          → TaskService.create()
4. HTTP POST               → /api/tasks
5. Route validates         → Zod schema
6. Service creates         → taskService.createTask()
7. Model saves             → TaskModel.create()
8. Response sent           → { success: true, data: task }
9. UI updates              → Task appears in list
```

## Error Handling

### Frontend
- HTTP errors caught in services
- User-friendly messages shown in UI
- Loading states during operations

### Backend
- Global error middleware catches all errors
- Structured error responses with codes
- Logging for debugging (no sensitive data)
