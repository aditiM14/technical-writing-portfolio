# API Documentation - TaskFlow

## Base URL

```
https://api.taskflow.com/v1
```

## Authentication

All API requests require authentication using a Bearer token.

### Header

```
Authorization: Bearer <your_access_token>
```

## 1. Create Task

### Endpoint: Create Task

### Description

Creates a new task in TaskFlow.

### Method

POST

### URL

```
/tasks
```

### Request Headers

```
Authorization: Bearer <your_token>
Content-Type: application/json
```

### Request Body

```json
{
  "title":"Complete documentation",
  "description":"Write API documentation for TaskFlow",
  "due_date":"2026-04-10",
  "priority":"High"
}
```

### Field Description

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| title | string | Yes | Task title |
| description | string | No | Task details |
| due_date | string | No | Due date (YYYY-MM-DD) |
| priority | string | No | Low, Medium, High |

### Example Request

```bash
curl-X POST https://api.taskflow.com/v1/tasks \
-H"Authorization: Bearer your_token" \
-H"Content-Type: application/json" \
-d'{
  "title": "Complete documentation",
  "description": "Write API documentation",
  "due_date": "2026-04-10",
  "priority": "High"
}'
```

### Example Response

```json
{
  "id":"12345",
  "title":"Complete documentation",
  "description": "Write API documentation",
  "status":"To Do",
  "priority": "High",
  "created_at":"2026-04-09T10:00:00Z"
}
```

### Status Codes

- 201 Created - Task created successfully
- 400 Bad Request - Invalid input
- 401 Unauthorized - Invalid token

## 2. Get All Tasks

### Endpoint: Get Tasks

### Description

Retrieves a list of all tasks.

### Method

GET

### URL

```
/tasks
```

### Request Headers

```
Authorization: Bearer <your_token>
```

### Example Request

```bash
curl-X GET https://api.taskflow.com/v1/tasks \
-H"Authorization: Bearer your_token"
```

### Example Response

```json
[
  {
    "id":"12345",
    "title":"Complete documentation",
    "status":"In Progress",
    "priority": "High"
  },
  {
    "id":"12346",
    "title":"Review tasks",
    "status":"To Do",
    "priority": "Medium"
  }
]
```

### Status Codes

- 200 OK - Success
- 401 Unauthorized - Invalid token

## 3. Update Task

### Endpoint: Update Task

### Description

Updates an existing task.

### Method

PUT

### URL

```
/tasks/{task_id}
```

### Path Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| task_id | string | Unique task ID |

### Request Body

```json
{
  "status":"Completed",
  "priority": "Low"
}
```

### Example Request

```bash
curl -X PUT https://api.taskflow.com/v1/tasks/task_001 \
-H "Authorization: Bearer your_access_token" \
-H "Content-Type: application/json" \
-d '{
  "status": "Completed",
  "priority": "Low"
}'
```

### Example Response

```json
{
  "message":"Task updated successfully"
}
```

### Status Codes

- 200 OK - Success
- 404 Not Found - Invalid Input
- 401 Unauthorized - Invalid Token

## 4. Delete Task

### Endpoint: Delete Task

### Description

Deletes a task.

### Method

DELETE

### URL

```
/tasks/{task_id}
```

### Path Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| task_id | string | Unique task ID |

### Example Request

```bash
curl-X DELETE https://api.taskflow.com/v1/tasks/12345 \
-H"Authorization: Bearer your_access_token"
```

### Example Response

```json
{
  "message":"Task deleted successfully"
}
```

### Status Codes

- 200 OK - Success
- 404 Not Found - Invalid Input
- 401 Unauthorized - Invalid Token