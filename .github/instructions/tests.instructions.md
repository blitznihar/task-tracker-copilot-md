---
applyTo: "**/*.test.ts,**/*.spec.ts"
---

# Test Instructions

## General Principles

- Test behavior, not implementation details.
- Cover happy path, validation failure, and edge cases.
- Use descriptive test names in `it('should ...')` style.
- Avoid brittle assertions tied to internal refactoring.
- Prefer test fixtures/builders for repeated setup.

## Test Structure

```typescript
describe('TaskService', () => {
  describe('createTask', () => {
    it('should create a task with valid input', async () => {
      // Arrange
      const input = { title: 'Test task', priority: 'medium' };
      
      // Act
      const result = await taskService.createTask(input);
      
      // Assert
      expect(result.title).toBe('Test task');
      expect(result.completed).toBe(false);
    });

    it('should throw ValidationError when title is empty', async () => {
      const input = { title: '', priority: 'medium' };
      await expect(taskService.createTask(input)).rejects.toThrow();
    });
  });
});
```

## Backend Tests (Jest)

- Use supertest for HTTP integration tests.
- Use mongodb-memory-server for database tests.
- Mock external services.
- Clean up test data after each test.

```typescript
// Integration test example
describe('POST /api/tasks', () => {
  it('should create a task and return 201', async () => {
    const response = await request(app)
      .post('/api/tasks')
      .send({ title: 'New task', priority: 'high' })
      .expect(201);
    
    expect(response.body.success).toBe(true);
    expect(response.body.data.title).toBe('New task');
  });
});
```

## Frontend Tests (Angular)

- Use Angular TestBed for component tests.
- Use HttpClientTestingModule for HTTP mocks.
- Test user interactions, not internal state.

```typescript
// Component test example
describe('TaskFormComponent', () => {
  it('should disable submit button when form is invalid', () => {
    const submitButton = fixture.debugElement.query(By.css('button[type="submit"]'));
    expect(submitButton.nativeElement.disabled).toBe(true);
  });
});
```

## What to Test

### Services
- Input validation
- Business logic branches
- Error handling
- Edge cases (empty arrays, null values)

### Routes/Controllers
- Successful requests (200, 201)
- Validation errors (400)
- Not found errors (404)
- Server errors (500)

### Components
- Rendering with different inputs
- User interactions (click, type, submit)
- Loading and error states

## What NOT to Test

- Third-party library internals
- Exact CSS class names (unless critical)
- Implementation details that may change
- Private methods directly
