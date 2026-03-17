# Create Angular Component

Build a new Angular component for the Task Tracker frontend.

## Inputs Needed

- Component name and purpose
- User interactions
- Data requirements (inputs/outputs)
- Validation rules (if form)

## Instructions

1. Read `docs/product-spec.md` for feature requirements.
2. Read `.github/instructions/frontend.instructions.md` for Angular patterns.
3. Create a standalone Angular component with OnPush change detection.
4. Use reactive forms for any form inputs.
5. Include proper validation and error messages.
6. Handle loading, error, and success states.
7. Keep business logic in services.
8. Reuse shared types from `packages/shared`.
9. Add component tests.

## Implementation Checklist

- [ ] Standalone component with `standalone: true`
- [ ] OnPush change detection
- [ ] Reactive forms with FormBuilder (if form)
- [ ] Input/Output decorators for data flow
- [ ] Loading state indicator
- [ ] Error state handling
- [ ] Accessibility (labels, ARIA, keyboard)
- [ ] SCSS styles with BEM naming
- [ ] Component tests

## File Structure

```
apps/web/src/app/components/[component-name]/
├── [component-name].component.ts
├── [component-name].component.html
├── [component-name].component.scss
└── [component-name].component.spec.ts
```

## Output Format

After implementation, provide:
- List of changed files
- User flow summary
- Accessibility considerations
- Tests added

## Example Usage

```
Using .github/prompts/create-angular-component.prompt.md:

Create a TaskFormComponent that:
- Has fields for title, description, due date, priority
- Validates title (required, 3-100 chars)
- Shows inline validation errors
- Emits (taskCreated) event on success
- Has a cancel button that emits (cancelled)
```
