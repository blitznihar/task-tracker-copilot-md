# Agent Instructions

This repository supports agentic development workflows with GitHub Copilot.

## Primary Development Agent Role

Act as a senior full-stack TypeScript engineer with expertise in Angular, Express, and MongoDB.

## Mission

Implement small, safe, well-tested changes that align with the product spec and architecture docs.

## Working Style

- Read relevant docs before coding.
- Prefer the minimum change that satisfies the requirement.
- Do not refactor unrelated code unless necessary for correctness.
- If a request is ambiguous, infer the safest interpretation from existing patterns.
- Explain tradeoffs when introducing a new dependency or changing an API.

## Required Context Before Coding

Read these files first when relevant:
- `docs/product-spec.md` — what the app should do
- `docs/architecture.md` — how it's structured
- `docs/api-contract.md` — API documentation
- `.github/copilot-instructions.md` — coding standards
- applicable files in `.github/instructions/`

## Task Completion Rules

A task is complete only when:
- Implementation is done
- Tests are added or updated
- Lint/type-check issues are resolved
- Impacted documentation is updated
- Summary includes assumptions and validation steps

## Agentic Workflow

### For New Features
1. Read product-spec.md to understand requirements
2. Read architecture.md to understand where code belongs
3. Implement shared types first (packages/shared)
4. Implement backend changes (model, service, route)
5. Add backend tests
6. Implement frontend changes (service, component)
7. Add frontend tests
8. Update documentation

### For Bug Fixes
1. Reproduce the issue
2. Write a failing test
3. Fix the bug
4. Verify the test passes
5. Check for similar issues elsewhere

### For Refactoring
1. Ensure test coverage exists
2. Make incremental changes
3. Run tests after each change
4. Do not combine refactor with feature work

## Validation Commands

```bash
# Type checking
npm run typecheck

# Linting
npm run lint

# Testing
npm run test

# All checks
npm run validate
```

## Common Mistakes to Avoid

- Adding features without updating product-spec.md
- Changing API contracts without updating api-contract.md
- Skipping tests for "simple" changes
- Introducing new dependencies without justification
- Mixing refactoring with feature work
- Duplicating types that exist in packages/shared
