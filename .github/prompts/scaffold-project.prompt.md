# Scaffold Task Tracker Project

Initialize the complete Task Tracker monorepo structure.

## Instructions

1. Read `docs/architecture.md` for the project structure.
2. Read `.github/copilot-instructions.md` for tech stack details.

## Step 1: Create Root Configuration

Create these files in the root:
- `package.json` with npm workspaces for apps/api, apps/web, packages/shared
- `tsconfig.base.json` with shared TypeScript settings
- `.gitignore` for Node.js projects
- `.nvmrc` with Node 18

## Step 2: Create Shared Package

In `packages/shared/`:
- `package.json` with name `@task-tracker/shared`
- `tsconfig.json` extending base config
- `src/types.ts` with Task, CreateTaskInput, UpdateTaskInput, TaskPriority, ApiResponse types
- `src/validators.ts` with Zod schemas for task validation
- `src/index.ts` exporting everything

## Step 3: Create Backend API

In `apps/api/`:
- `package.json` with Express, Mongoose, Zod, cors, helmet, dotenv
- `tsconfig.json` extending base config
- `.env.example` with MONGODB_URI, PORT, CORS_ORIGIN
- `src/index.ts` - Express app entry point
- `src/config/database.ts` - MongoDB connection
- `src/models/task.model.ts` - Mongoose Task schema
- `src/services/task.service.ts` - Business logic
- `src/routes/tasks.routes.ts` - CRUD endpoints
- `src/middleware/error.middleware.ts` - Error handling

## Step 4: Create Angular Frontend

In `apps/web/`:
- Use Angular CLI: `ng new web --standalone --routing --style=scss`
- Configure proxy to backend API
- Create environment files

## Output

List all created files and provide commands to:
1. Install dependencies
2. Start MongoDB
3. Run backend
4. Run frontend
