# GitHub Copilot MD Files Guide

## Overview

This guide explains each Markdown file's purpose, when it's automatically applied, and when you should manually reference it.

---

## 1. Repository-Wide Instructions

### File: `.github/copilot-instructions.md`

**Purpose**: Global coding standards that apply to ALL code in the repository.

**When it's used**: 
- ✅ **Automatically** — Copilot reads this file for every request
- No need to manually reference it

**What to include**:
- Tech stack definition (Angular, Node.js, MongoDB)
- Coding standards (TypeScript strict mode, no `any`)
- Architecture rules (where code belongs)
- Quality rules (testing, documentation)
- Safety rules (no hardcoded secrets)
- Environment variables list

**Example scenario**:
> You ask Copilot to "create a new service"
> → Copilot automatically applies rules from this file
> → Uses TypeScript, follows naming conventions, adds tests

---

## 2. Path-Specific Instructions

### Files: `.github/instructions/*.instructions.md`

| File | Applies To | Purpose |
|------|-----------|---------|
| `frontend.instructions.md` | `apps/web/**` | Angular patterns, component structure |
| `backend.instructions.md` | `apps/api/**` | Express patterns, API response format |
| `tests.instructions.md` | `**/*.test.ts`, `**/*.spec.ts` | Testing patterns, what to test |
| `docs.instructions.md` | `docs/**`, `README.md` | Documentation style |

**When they're used**:
- ✅ **Automatically** — Applied based on the `applyTo` path pattern in frontmatter
- When you're working on a file matching the pattern, Copilot loads the relevant instructions

**Example scenario**:
> You're editing `apps/web/src/app/components/task-form.component.ts`
> → Copilot automatically loads `frontend.instructions.md`
> → Suggests standalone components, OnPush change detection, reactive forms

**When to manually reference**:
```
Read .github/instructions/backend.instructions.md and create a new endpoint
```
Use this when you want Copilot to pay extra attention to specific patterns.

---

## 3. Reusable Prompt Files

### Files: `.github/prompts/*.prompt.md`

| File | Use Case |
|------|----------|
| `scaffold-project.prompt.md` | Initialize the entire monorepo |
| `create-api-endpoint.prompt.md` | Add a new REST endpoint |
| `create-angular-component.prompt.md` | Build a new Angular component |
| `write-tests.prompt.md` | Generate tests from acceptance criteria |
| `refactor-safely.prompt.md` | Refactor without breaking behavior |

**When they're used**:
- ❌ **Never automatic** — You must explicitly invoke them
- These are templates for common, repeatable tasks

**How to use**:
```
Use .github/prompts/create-api-endpoint.prompt.md to create:
- DELETE /api/tasks/:id endpoint
- Return 204 on success, 404 if not found
```

**Why they exist**:
- Consistency across similar tasks
- Checklist ensures nothing is missed (validation, tests, docs)
- Saves time explaining the same requirements repeatedly

---

## 4. Documentation Files

### Files: `docs/*.md`

| File | Contains | Copilot Uses It For |
|------|----------|---------------------|
| `product-spec.md` | Features, acceptance criteria | Understanding WHAT to build |
| `architecture.md` | System design, layers, data flow | Understanding WHERE code goes |
| `api-contract.md` | Endpoints, request/response shapes | API implementation details |
| `definition-of-done.md` | Completion checklist | Knowing when work is complete |

**When they're used**:
- ❌ **Not automatic** — You should reference them before major tasks
- They're the "source of truth" that prevents Copilot from guessing

**How to use**:
```
Read docs/product-spec.md and docs/architecture.md.
Then implement the "filter tasks" feature following the acceptance criteria.
```

**Why they matter**:
- Without specs, Copilot invents requirements
- Without architecture docs, Copilot puts code in wrong places
- With docs, Copilot generates code that fits your design

---

## 5. Agent Instructions

### File: `AGENTS.md`

**Purpose**: Instructions for when Copilot operates in "agentic" mode — autonomously completing multi-step tasks.

**When it's used**:
- Copilot reads this when running multi-file, multi-step operations
- Defines workflow order (shared → backend → frontend → tests → docs)
- Sets completion criteria

**What it contains**:
- Role definition ("senior full-stack TypeScript engineer")
- Working style (minimal changes, read docs first)
- Task completion rules
- Validation commands

---

## Quick Reference: When to Reference What

| You Want To... | Reference These Files |
|----------------|----------------------|
| Start a new feature | `docs/product-spec.md` + `docs/architecture.md` |
| Create an API endpoint | `.github/prompts/create-api-endpoint.prompt.md` + `docs/api-contract.md` |
| Create a component | `.github/prompts/create-angular-component.prompt.md` |
| Write tests | `.github/prompts/write-tests.prompt.md` + `docs/product-spec.md` |
| Refactor code | `.github/prompts/refactor-safely.prompt.md` |
| Review generated code | `.github/copilot-instructions.md` + relevant path instruction |
| Initialize project | `.github/prompts/scaffold-project.prompt.md` |

---

## The Hierarchy

```
┌─────────────────────────────────────────────────────────┐
│  .github/copilot-instructions.md                        │
│  (ALWAYS active - global rules)                         │
├─────────────────────────────────────────────────────────┤
│  .github/instructions/*.instructions.md                 │
│  (AUTO-APPLIED based on file path)                      │
├─────────────────────────────────────────────────────────┤
│  docs/*.md                                              │
│  (REFERENCE before major tasks - source of truth)       │
├─────────────────────────────────────────────────────────┤
│  .github/prompts/*.prompt.md                            │
│  (INVOKE for repeatable workflows)                      │
├─────────────────────────────────────────────────────────┤
│  AGENTS.md                                              │
│  (READ by Copilot for multi-step autonomous tasks)      │
└─────────────────────────────────────────────────────────┘
```

---

## Sample Workflow

### Adding a "Delete Task" Feature

1. **Start by reading docs**:
   ```
   Read docs/product-spec.md and docs/api-contract.md.
   I need to implement the delete task feature.
   ```

2. **Use prompt for backend**:
   ```
   Use .github/prompts/create-api-endpoint.prompt.md to create:
   DELETE /api/tasks/:id
   - Validate ID format
   - Return 404 if not found
   - Return 204 on success
   ```

3. **Use prompt for frontend**:
   ```
   Use .github/prompts/create-angular-component.prompt.md to add
   a delete button to TaskItemComponent with confirmation dialog.
   ```

4. **Generate tests**:
   ```
   Use .github/prompts/write-tests.prompt.md for the delete feature.
   Cover: successful deletion, not found, invalid ID.
   ```

5. **Review against standards**:
   ```
   Review all changes against .github/copilot-instructions.md
   and list any violations.
   ```

---

## Adding to README.md

Add this section to your project's README.md:

```markdown
## Using GitHub Copilot

This repository is optimized for GitHub Copilot with structured guidance files.

### Quick Start

1. Open Copilot Chat (`Ctrl+Shift+I` / `Cmd+Shift+I`)
2. Start with: "Read docs/product-spec.md and docs/architecture.md"
3. Use prompt files for common tasks

### File Reference

| File Type | Location | When Used |
|-----------|----------|-----------|
| Global rules | `.github/copilot-instructions.md` | Always (automatic) |
| Path rules | `.github/instructions/` | Auto-applied by file path |
| Task prompts | `.github/prompts/` | Invoke manually |
| Specs & docs | `docs/` | Reference before coding |
| Agent guide | `AGENTS.md` | Multi-step tasks |

### Common Prompts

- **New endpoint**: `Use .github/prompts/create-api-endpoint.prompt.md`
- **New component**: `Use .github/prompts/create-angular-component.prompt.md`
- **Write tests**: `Use .github/prompts/write-tests.prompt.md`
- **Refactor**: `Use .github/prompts/refactor-safely.prompt.md`
```
