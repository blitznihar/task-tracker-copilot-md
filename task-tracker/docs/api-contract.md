# API Contract

Base URL: `http://localhost:3000/api`

## Response Format

### Success Response

```json
{
  "success": true,
  "data": { ... }
}
```

### Error Response

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable message",
    "details": { "field": "Error for this field" }
  }
}
```

## Error Codes

| Code | HTTP Status | Description |
|------|-------------|-------------|
| VALIDATION_ERROR | 400 | Invalid request data |
| NOT_FOUND | 404 | Resource not found |
| INTERNAL_ERROR | 500 | Server error |

---

## Endpoints

### GET /api/tasks

Retrieve all tasks, optionally filtered.

**Query Parameters**

| Parameter | Type | Required | Values |
|-----------|------|----------|--------|
| status | string | No | `all`, `active`, `completed` |
| priority | string | No | `low`, `medium`, `high` |

**Response 200**

```json
{
  "success": true,
  "data": [
    {
      "id": "65f1a2b3c4d5e6f7g8h9i0j1",
      "title": "Pay electricity bill",
      "description": "Before Friday",
      "dueDate": "2026-03-20",
      "priority": "high",
      "completed": false,
      "createdAt": "2026-03-15T10:30:00.000Z",
      "updatedAt": "2026-03-15T10:30:00.000Z"
    }
  ]
}
```

---

### GET /api/tasks/:id

Retrieve a single task by ID.

**Response 200**

```json
{
  "success": true,
  "data": {
    "id": "65f1a2b3c4d5e6f7g8h9i0j1",
    "title": "Pay electricity bill",
    "description": "Before Friday",
    "dueDate": "2026-03-20",
    "priority": "high",
    "completed": false,
    "createdAt": "2026-03-15T10:30:00.000Z",
    "updatedAt": "2026-03-15T10:30:00.000Z"
  }
}
```

**Response 404**

```json
{
  "success": false,
  "error": {
    "code": "NOT_FOUND",
    "message": "Task not found"
  }
}
```

---

### POST /api/tasks

Create a new task.

**Request Body**

```json
{
  "title": "Pay electricity bill",
  "description": "Before Friday",
  "dueDate": "2026-03-20",
  "priority": "high"
}
```

**Validation Rules**

| Field | Type | Required | Rules |
|-------|------|----------|-------|
| title | string | Yes | 3-100 characters |
| description | string | No | Max 500 characters |
| dueDate | string | No | ISO date, today or future |
| priority | string | Yes | `low`, `medium`, or `high` |

**Response 201**

```json
{
  "success": true,
  "data": {
    "id": "65f1a2b3c4d5e6f7g8h9i0j1",
    "title": "Pay electricity bill",
    "description": "Before Friday",
    "dueDate": "2026-03-20",
    "priority": "high",
    "completed": false,
    "createdAt": "2026-03-15T10:30:00.000Z",
    "updatedAt": "2026-03-15T10:30:00.000Z"
  }
}
```

**Response 400**

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation failed",
    "details": {
      "title": "Title must be between 3 and 100 characters"
    }
  }
}
```

---

### PUT /api/tasks/:id

Update an existing task.

**Request Body**

```json
{
  "title": "Pay electricity bill - URGENT",
  "description": "Before Thursday",
  "dueDate": "2026-03-19",
  "priority": "high",
  "completed": true
}
```

**Response 200**

```json
{
  "success": true,
  "data": {
    "id": "65f1a2b3c4d5e6f7g8h9i0j1",
    "title": "Pay electricity bill - URGENT",
    "completed": true,
    "updatedAt": "2026-03-15T14:45:00.000Z"
  }
}
```

---

### PATCH /api/tasks/:id/toggle

Toggle the completion status of a task.

**Response 200**

```json
{
  "success": true,
  "data": {
    "id": "65f1a2b3c4d5e6f7g8h9i0j1",
    "completed": true,
    "updatedAt": "2026-03-15T14:45:00.000Z"
  }
}
```

---

### DELETE /api/tasks/:id

Delete a task.

**Response 204**

No content.

**Response 404**

```json
{
  "success": false,
  "error": {
    "code": "NOT_FOUND",
    "message": "Task not found"
  }
}
```
