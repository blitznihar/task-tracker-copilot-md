# Definition of Done

A task is considered **done** when all applicable criteria are met.

## Code Changes

- [ ] Implementation satisfies the requirements
- [ ] Code follows project conventions (see `.github/copilot-instructions.md`)
- [ ] No `any` types unless explicitly justified
- [ ] No hardcoded values that should be configurable
- [ ] Error handling is in place

## Testing

- [ ] Unit tests added/updated for services
- [ ] Integration tests added/updated for routes (backend)
- [ ] Component tests added/updated (frontend)
- [ ] All tests pass: `npm run test`
- [ ] Edge cases covered

## Code Quality

- [ ] Type-check passes: `npm run typecheck`
- [ ] Lint passes: `npm run lint`
- [ ] No new warnings introduced

## Documentation

- [ ] API changes reflected in `docs/api-contract.md`
- [ ] Feature changes reflected in `docs/product-spec.md`
- [ ] Architecture changes reflected in `docs/architecture.md`

## Accessibility (Frontend)

- [ ] Keyboard navigation works
- [ ] ARIA labels verified
- [ ] Focus states visible

## Final Checklist

- [ ] Ran full validation: `npm run validate`
- [ ] Summarized changes
- [ ] Listed assumptions
- [ ] Identified follow-up items (if any)
