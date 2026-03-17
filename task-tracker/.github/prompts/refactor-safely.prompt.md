# Refactor Safely

Refactor code without changing external behavior.

## Inputs Needed

- Code to refactor
- Reason for refactoring
- Constraints to preserve

## Instructions

1. Verify test coverage exists before refactoring.
2. If coverage is weak, add tests first.
3. Preserve public contracts (APIs, component interfaces).
4. Keep changes minimal and reversible.
5. Explain why the refactor improves maintainability.
6. Do not combine refactor and feature work.

## Refactoring Types

### Extract
- Extract function for repeated logic
- Extract component for repeated UI
- Extract service for shared behavior

### Rename
- Improve clarity of names
- Align with domain terminology

### Restructure
- Move code to better location
- Split large files
- Consolidate related code

### Simplify
- Remove dead code
- Simplify complex conditionals
- Replace imperative with declarative

## Safety Checklist

- [ ] Tests pass before refactoring
- [ ] Each change is independently testable
- [ ] Tests pass after each change
- [ ] Public interfaces unchanged
- [ ] No feature changes mixed in

## Output Format

After refactoring, provide:
- List of changed files
- What was refactored and why
- Tests that verify behavior preserved
- Any risks or follow-ups

## Example Usage

```
Using .github/prompts/refactor-safely.prompt.md:

Refactor TaskService.getFilteredTasks():
- Extract filter logic into separate pure functions
- Make the main function easier to read
- Preserve current filtering behavior exactly
```
