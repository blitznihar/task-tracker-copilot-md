# Task Tracker Product Spec

## Overview

Task Tracker is a personal task management application that helps users organize, track, and complete their tasks efficiently.

## Core Features

1. **Create task** — User can create a task with title, description, due date, and priority.
2. **Complete task** — User can mark a task as complete or incomplete.
3. **Edit task** — User can edit an existing task.
4. **Delete task** — User can delete a task.
5. **Filter tasks** — User can filter tasks by status and priority.
6. **View tasks** — User can view all tasks in a list.

## Acceptance Criteria

### Create Task

| Criteria | Details |
|----------|---------|
| Title required | Cannot be empty |
| Title length | 3 to 100 characters |
| Description | Optional, max 500 characters |
| Due date | Optional, must be today or future |
| Priority | Required, one of: `low`, `medium`, `high` |
| Default state | New tasks are not completed |
| Success feedback | New task appears in list immediately |
| Error feedback | Validation errors shown inline |

### Complete Task

| Criteria | Details |
|----------|---------|
| Toggle action | Click checkbox or toggle button |
| Visual feedback | Completed tasks show strikethrough and muted style |
| Persistence | State saved to database |
| Reversible | Can mark incomplete again |

### Edit Task

| Criteria | Details |
|----------|---------|
| Editable fields | Title, description, due date, priority |
| Validation | Same rules as create |
| Preservation | Completion state preserved |
| Success feedback | Changes reflected immediately |

### Delete Task

| Criteria | Details |
|----------|---------|
| Confirmation | Show confirm dialog before deletion |
| Removal | Task removed from list |
| Irreversible | Cannot undo |

### Filter Tasks

| Criteria | Details |
|----------|---------|
| Status filter | All, Active, Completed |
| Priority filter | All, Low, Medium, High |
| Combination | Filters can be combined |
| Empty state | Show message when no tasks match |

## Non-Functional Requirements

### Accessibility
- Keyboard navigation for all actions
- Screen reader compatible
- Focus management on modals/dialogs
- Color contrast meets WCAG AA

### Performance
- Initial load under 3 seconds
- Task operations feel instant (<200ms)

### Responsive Design
- Works on mobile (320px+)
- Works on tablet (768px+)
- Works on desktop (1024px+)

### Data Integrity
- Strong typing across stack
- Validation on both client and server
- No silent failures

## Out of Scope (v1)

- User authentication
- Multiple task lists
- Task categories/tags
- Recurring tasks
- Task sharing
- File attachments
- Notifications/reminders
