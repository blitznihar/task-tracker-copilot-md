# Write Tests

Write or update tests for a feature or file based on acceptance criteria.

## Inputs Needed

- Feature or file to test
- Acceptance criteria from product spec
- Edge cases to consider

## Instructions

1. Read `docs/product-spec.md` for acceptance criteria.
2. Read `.github/instructions/tests.instructions.md` for testing patterns.
3. Identify expected behavior from acceptance criteria.
4. Identify failure cases and edge cases.
5. Write tests that verify externally visible behavior.
6. Avoid mocking more than necessary.
7. Call out gaps if acceptance criteria are unclear.

## Test Categories

### Happy Path
- Valid input produces expected output
- State changes correctly
- Events fire as expected

### Validation Failures
- Missing required fields
- Invalid field values
- Boundary conditions (min/max length)

### Edge Cases
- Empty collections
- Maximum values
- Null/undefined handling

## Backend Test Template

```typescript
describe('TaskService', () => {
  beforeEach(async () => {
    // Setup test database
  });

  afterEach(async () => {
    // Cleanup
  });

  describe('createTask', () => {
    it('should create a task with valid input', async () => {
      // Arrange, Act, Assert
    });

    it('should reject empty title', async () => {
      // Test validation
    });
  });
});
```

## Frontend Test Template

```typescript
describe('TaskFormComponent', () => {
  let component: TaskFormComponent;
  let fixture: ComponentFixture<TaskFormComponent>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      imports: [TaskFormComponent]
    }).compileComponents();
  });

  it('should disable submit when form is invalid', () => {
    // Test UI state
  });
});
```

## Output Format

- List of test files changed
- Summary of test scenarios covered
- Coverage gaps identified
