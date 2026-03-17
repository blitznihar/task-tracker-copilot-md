# Create API Endpoint

Create a new Express endpoint for the Task Tracker API.

## Inputs Needed

- Endpoint purpose
- HTTP method and path
- Request shape (body, params, query)
- Response shape
- Validation rules
- Business logic / service behavior

## Instructions

1. Read `docs/api-contract.md` for existing endpoints and response format.
2. Read `.github/instructions/backend.instructions.md` for patterns.
3. Create or update the Mongoose model if needed.
4. Create or update the service with business logic.
5. Implement route handler with Zod validation.
6. Reuse shared types and validators from `packages/shared`.
7. Add tests for success and failure cases.
8. Update `docs/api-contract.md` with the new endpoint.

## Implementation Checklist

- [ ] Request validation using Zod
- [ ] Proper HTTP status codes (200, 201, 400, 404, 500)
- [ ] Consistent response format `{ success, data/error }`
- [ ] Error handling with try/catch
- [ ] Unit tests for service
- [ ] Integration tests for route
- [ ] API documentation updated

## Output Format

After implementation, provide:
- List of changed files
- Endpoint behavior summary
- Test coverage summary
- Assumptions made

## Example Usage

```
Using .github/prompts/create-api-endpoint.prompt.md:

Create a PATCH /api/tasks/:id/toggle endpoint that:
- Validates the task ID format (MongoDB ObjectId)
- Returns 404 if task not found
- Toggles the completed boolean
- Returns the updated task
```
