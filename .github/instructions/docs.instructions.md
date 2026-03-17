---
applyTo: "docs/**,README.md"
---

# Documentation Instructions

## Writing Style

- Write concise, developer-friendly documentation.
- Keep examples aligned with the actual codebase.
- Use present tense ("The API returns..." not "The API will return...").
- Prefer active voice.

## When APIs Change

- Update request and response examples in `docs/api-contract.md`.
- Update the endpoint table in README.md.
- Note breaking changes prominently.
- Include migration steps if needed.

## Structure

- Prefer short sections with clear headings.
- Use code blocks for examples.
- Include both success and error response examples.
- Call out assumptions, limitations, and next steps.

## API Documentation (api-contract.md)

For each endpoint, document:
- HTTP method and path
- Request body schema
- Response schema (success and error)
- Example request/response
- Validation rules
- Error codes

## README Updates

When updating README.md:
- Keep the quick start guide current.
- Update the features list when adding features.
- Verify all commands still work.
- Update environment variable documentation.
