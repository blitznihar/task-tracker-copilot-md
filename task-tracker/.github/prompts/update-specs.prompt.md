# Update Specs and Contracts

Use this prompt when adding, removing, or modifying features in the Task Tracker.

## When to Use

- Adding a new feature
- Removing a deprecated feature
- Changing acceptance criteria
- Modifying API endpoints
- Updating validation rules

## Workflow

### Step 1: Update Documentation First

Always update docs BEFORE writing code. This keeps Copilot aligned.

**For new features:**
1. Add to `docs/product-spec.md` — acceptance criteria
2. Add to `docs/api-contract.md` — new endpoints (if any)
3. Update `docs/architecture.md` — if architecture changes

**For removed features:**
1. Mark as deprecated or remove from `docs/product-spec.md`
2. Remove endpoints from `docs/api-contract.md`
3. Note breaking changes

**For modified features:**
1. Update acceptance criteria in `docs/product-spec.md`
2. Update request/response shapes in `docs/api-contract.md`
3. Note if breaking change

### Step 2: Ask Copilot to Implement

After updating docs, ask Copilot:

```
Read the updated docs/product-spec.md and docs/api-contract.md.
Implement the changes for [feature name].
Update existing code to match the new spec.
Add/update tests for changed behavior.
```

### Step 3: Verify Against Updated Docs

```
Review the implementation against:
- docs/product-spec.md (acceptance criteria)
- docs/api-contract.md (API shapes)
- docs/definition-of-done.md (completion checklist)

List any gaps or inconsistencies.
```

## Example: Adding "Task Categories" Feature

### 1. Update product-spec.md

Add this section:

```markdown
### Categories (NEW)

| Criteria | Details |
|----------|---------|
| Create category | Name required, 2-50 characters |
| Assign to task | Optional, one category per task |
| Filter by category | Show tasks in selected category |
| Default | "Uncategorized" if none assigned |
```

### 2. Update api-contract.md

Add new endpoints:

```markdown
### GET /api/categories

List all categories.

**Response 200**
{ "success": true, "data": [{ "id": "...", "name": "Work" }] }

### POST /api/categories

Create a category.

**Request**
{ "name": "Work" }

**Response 201**
{ "success": true, "data": { "id": "...", "name": "Work" } }
```

Update existing task endpoints to include `categoryId`.

### 3. Update architecture.md (if needed)

Add category model to the structure diagram.

### 4. Ask Copilot to Implement

```
Read the updated docs/product-spec.md and docs/api-contract.md.

I've added a Categories feature. Implement:
1. Category model in packages/shared
2. Category endpoints in apps/api
3. Category service and components in apps/web
4. Update Task model to include optional categoryId
5. Add tests for new functionality
```

## Example: Removing "Due Date" Field

### 1. Update product-spec.md

Remove or strike through due date references:

```markdown
### Create Task

| Criteria | Details |
|----------|---------|
| Title required | Cannot be empty |
| Title length | 3 to 100 characters |
| Description | Optional, max 500 characters |
| ~~Due date~~ | ~~Optional, must be today or future~~ REMOVED |
| Priority | Required, one of: low, medium, high |
```

### 2. Update api-contract.md

Remove `dueDate` from request/response examples.

### 3. Ask Copilot to Implement

```
Read the updated docs/product-spec.md and docs/api-contract.md.

The dueDate field has been removed from tasks. Update:
1. Remove dueDate from Task type in packages/shared
2. Remove dueDate validation
3. Remove dueDate from API endpoints
4. Remove dueDate input from TaskFormComponent
5. Update tests to remove dueDate assertions
6. Note: This is a breaking change for existing data
```

## Example: Modifying Validation Rules

### 1. Update product-spec.md

Change the rule:

```markdown
| Title length | ~~3 to 100 characters~~ → 1 to 200 characters |
```

### 2. Update api-contract.md

Update validation rules table.

### 3. Ask Copilot to Implement

```
Read the updated docs/product-spec.md and docs/api-contract.md.

Title validation has changed from 3-100 to 1-200 characters.
Update:
1. Zod schema in packages/shared/validators.ts
2. Frontend form validation in TaskFormComponent
3. Update tests for new boundary values (1 char, 200 chars)
```

## Checklist for Spec Changes

- [ ] Updated `docs/product-spec.md` with new/changed criteria
- [ ] Updated `docs/api-contract.md` with endpoint changes
- [ ] Updated `docs/architecture.md` if structure changed
- [ ] Noted breaking changes prominently
- [ ] Asked Copilot to implement against updated docs
- [ ] Verified implementation matches new specs
- [ ] Updated tests for changed behavior
- [ ] Checked `docs/definition-of-done.md` criteria
