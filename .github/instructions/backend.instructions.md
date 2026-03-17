---
applyTo: "apps/api/**"
---

# Backend Instructions (Express + MongoDB)

## Route Handlers

- Keep route handlers thin.
- Validate all request bodies, params, and query values using Zod.
- Put business rules in services.
- Return consistent JSON response shapes.
- Use explicit HTTP status codes.

## Response Format

All API responses must follow this structure:

```typescript
// Success response
{
  "success": true,
  "data": { ... }
}

// Error response
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Human-readable message",
    "details": { ... }  // Optional field-level errors
  }
}
```

## Error Handling

- Use custom error classes for different error types.
- Implement global error handling middleware.
- Log errors with appropriate context.
- Never expose stack traces in production.

## MongoDB/Mongoose

- Define schemas in `models/` directory.
- Use Mongoose validation for data integrity.
- Index frequently queried fields.
- Use lean queries when you don't need Mongoose documents.
- Transform `_id` to `id` in responses.

## Validation

- Use Zod schemas from `packages/shared` for request validation.
- Return 400 for validation errors with field details.
- Validate ObjectId format before database queries.

## Testing

- Add unit tests for services.
- Add integration tests for routes using supertest.
- Use mongodb-memory-server for database tests.
- Test success, failure, and edge cases.

## File Organization

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

## Code Patterns

```typescript
// Route handler pattern
router.post('/tasks', async (req, res, next) => {
  try {
    const input = createTaskSchema.parse(req.body);
    const task = await taskService.createTask(input);
    res.status(201).json({ success: true, data: task });
  } catch (error) {
    next(error);
  }
});

// Service pattern
export const taskService = {
  async createTask(input: CreateTaskInput): Promise<Task> {
    const task = await TaskModel.create(input);
    return transformTask(task);
  }
};

// Mongoose model pattern
const taskSchema = new Schema({
  title: { type: String, required: true },
  completed: { type: Boolean, default: false }
}, { timestamps: true });
```

## Security

- Sanitize user input.
- Use helmet for security headers.
- Implement rate limiting for production.
- Validate ObjectId format before queries.
