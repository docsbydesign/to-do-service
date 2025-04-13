# Task Management API Reference

**API Version:** 1.0.0

## Table of Contents

1. [Introduction](#introduction)
2. [Authentication](#authentication)
3. [Base URL](#base-url)
4. [Endpoints](#endpoints)
   - [User Operations](#user-operations)
   - [Task Operations](#task-operations)
5. [Data Models](#data-models)
6. [Examples](#examples)
7. [Error Handling](#error-handling)

## Introduction

The Task Management API provides a RESTful interface for managing users and their tasks. This API enables applications to create, read, update, and delete both users and tasks.

## Authentication

Authentication details are not specified in the current API specification.

## Base URL

The base URL for the API is not specified in the current specification. Please contact the API provider for the appropriate base URL for your environment.

## Endpoints

### User Operations

#### Get All Users

Retrieves a list of all users in the system.

```http
GET /users
```

**Response**

Status Code: `200 OK`

```json
{
  "users": [
    {
      "last_name": "Smith",
      "first_name": "Ferdinand",
      "email": "f.smith@example.com",
      "id": 1
    },
    {
      "last_name": "Jones",
      "first_name": "Jill",
      "email": "j.jones@example.com",
      "id": 2
    },
    // Additional users...
  ]
}
```

#### Add a User

Creates a new user in the system.

```http
POST /users
```

**Request Body**

```json
{
  "last_name": "Doe",
  "first_name": "John",
  "email": "j.doe@example.com"
}
```

**Response**

Status Code: `201 Created`

```json
{
  "id": 5,
  "last_name": "Doe",
  "first_name": "John",
  "email": "j.doe@example.com"
}
```

#### Get User by ID

Retrieves a specific user by their ID.

```http
GET /users/{userId}
```

**Path Parameters**

| Parameter | Type    | Required | Description    |
|-----------|---------|----------|----------------|
| userId    | integer | Yes      | ID of the user |

**Response**

Status Code: `200 OK`

```json
{
  "last_name": "Smith",
  "first_name": "Ferdinand",
  "email": "f.smith@example.com",
  "id": 1
}
```

#### Update User

Updates specific properties of a user, excluding their ID.

```http
PATCH /users/{userId}
```

**Path Parameters**

| Parameter | Type    | Required | Description    |
|-----------|---------|----------|----------------|
| userId    | integer | Yes      | ID of the user |

**Request Body**

```json
{
  "email": "new.email@example.com"
}
```

**Response**

Status Code: `200 OK`

```json
{
  "last_name": "Smith",
  "first_name": "Ferdinand",
  "email": "new.email@example.com",
  "id": 1
}
```

#### Delete User

Deletes a user from the system.

```http
DELETE /users/{userId}
```

**Path Parameters**

| Parameter | Type    | Required | Description    |
|-----------|---------|----------|----------------|
| userId    | integer | Yes      | ID of the user |

**Response**

Status Code: `204 No Content`

### Task Operations

#### Get All Tasks

Retrieves a list of all tasks in the system.

```http
GET /tasks
```

**Response**

Status Code: `200 OK`

```json
{
  "tasks": [
    {
      "user_id": 1,
      "title": "Grocery shopping",
      "description": "eggs, bacon, gummy bears",
      "due_date": "2024-02-20T17:00:00.000-05:00",
      "warning": -60,
      "id": 1
    },
    {
      "user_id": 1,
      "title": "Piano recital",
      "description": "Daughter's first concert appearance",
      "due_date": "2024-04-02T15:00:00-05:00",
      "warning": -30,
      "id": 2
    },
    // Additional tasks...
  ]
}
```

#### Add a Task

Creates a new task in the system.

```http
POST /tasks
```

**Request Body**

```json
{
  "user_id": 1,
  "title": "New Task",
  "description": "Description of the new task",
  "due_date": "2024-06-01T12:00:00-05:00",
  "warning": -5
}
```

**Response**

Status Code: `201 Created`

```json
{
  "id": 5,
  "user_id": 1,
  "title": "New Task",
  "description": "Description of the new task",
  "due_date": "2024-06-01T12:00:00-05:00",
  "warning": -5
}
```

#### Get Task by ID

Retrieves a specific task by its ID.

```http
GET /tasks/{taskId}
```

**Path Parameters**

| Parameter | Type    | Required | Description    |
|-----------|---------|----------|----------------|
| taskId    | integer | Yes      | ID of the task |

**Response**

Status Code: `200 OK`

```json
{
  "user_id": 1,
  "title": "Grocery shopping",
  "description": "eggs, bacon, gummy bears",
  "due_date": "2024-02-20T17:00:00-05:00",
  "warning": -10,
  "id": 1
}
```

#### Update Task

Updates specific properties of a task, excluding its ID.

```http
PATCH /tasks/{taskId}
```

**Path Parameters**

| Parameter | Type    | Required | Description    |
|-----------|---------|----------|----------------|
| taskId    | integer | Yes      | ID of the task |

**Request Body**

```json
{
  "description": "Updated description"
}
```

**Response**

Status Code: `200 OK`

```json
{
  "user_id": 1,
  "title": "Grocery shopping",
  "description": "Updated description",
  "due_date": "2024-02-20T17:00:00-05:00",
  "warning": -10,
  "id": 1
}
```

#### Delete Task

Deletes a task from the system.

```http
DELETE /tasks/{taskId}
```

**Path Parameters**

| Parameter | Type    | Required | Description    |
|-----------|---------|----------|----------------|
| taskId    | integer | Yes      | ID of the task |

**Response**

Status Code: `204 No Content`

## Data Models

### User

Represents a user in the system.

| Field      | Type    | Required | Description       |
|------------|---------|----------|-------------------|
| id         | integer | Yes      | Unique identifier |
| last_name  | string  | Yes      | User's last name  |
| first_name | string  | Yes      | User's first name |
| email      | string  | Yes      | User's email address (must be valid format) |

### UserInput

Represents the data required to create a new user.

| Field      | Type   | Required | Description       |
|------------|--------|----------|-------------------|
| last_name  | string | Yes      | User's last name  |
| first_name | string | Yes      | User's first name |
| email      | string | Yes      | User's email address (must be valid format) |

### UserPatch

Represents the data for updating a user. At least one property must be provided.

| Field      | Type   | Required | Description       |
|------------|--------|----------|-------------------|
| last_name  | string | No       | User's last name  |
| first_name | string | No       | User's first name |
| email      | string | No       | User's email address (must be valid format) |

### Task

Represents a task in the system.

| Field       | Type    | Required | Description                               |
|-------------|---------|----------|-------------------------------------------|
| id          | integer | Yes      | Unique identifier                         |
| user_id     | integer | Yes      | ID of the user associated with this task  |
| title       | string  | Yes      | Title of the task                         |
| description | string  | No       | Detailed description of the task          |
| due_date    | string  | Yes      | Due date and time of the task (ISO 8601 format) |
| warning     | integer | Yes      | Minutes before due date to issue warning  |

### TaskInput

Represents the data required to create a new task.

| Field       | Type    | Required | Description                               |
|-------------|---------|----------|-------------------------------------------|
| user_id     | integer | Yes      | ID of the user associated with this task  |
| title       | string  | Yes      | Title of the task                         |
| description | string  | No       | Detailed description of the task          |
| due_date    | string  | Yes      | Due date and time of the task (ISO 8601 format) |
| warning     | integer | Yes      | Minutes before due date to issue warning  |

### TaskPatch

Represents the data for updating a task. At least one property must be provided.

| Field       | Type    | Required | Description                               |
|-------------|---------|----------|-------------------------------------------|
| user_id     | integer | No       | ID of the user associated with this task  |
| title       | string  | No       | Title of the task                         |
| description | string  | No       | Detailed description of the task          |
| due_date    | string  | No       | Due date and time of the task (ISO 8601 format) |
| warning     | integer | No       | Minutes before due date to issue warning  |

## Examples

### Create a New User

**Request:**

```http
POST /users
Content-Type: application/json

{
  "last_name": "Doe",
  "first_name": "John",
  "email": "j.doe@example.com"
}
```

**Response:**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 5,
  "last_name": "Doe",
  "first_name": "John",
  "email": "j.doe@example.com"
}
```

### Create a New Task

**Request:**

```http
POST /tasks
Content-Type: application/json

{
  "user_id": 1,
  "title": "New Task",
  "description": "Description of the new task",
  "due_date": "2024-06-01T12:00:00-05:00",
  "warning": -5
}
```

**Response:**

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 5,
  "user_id": 1,
  "title": "New Task",
  "description": "Description of the new task",
  "due_date": "2024-06-01T12:00:00-05:00",
  "warning": -5
}
```

### Update a Task

**Request:**

```http
PATCH /tasks/1
Content-Type: application/json

{
  "description": "Updated description"
}
```

**Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "user_id": 1,
  "title": "Grocery shopping",
  "description": "Updated description",
  "due_date": "2024-02-20T17:00:00-05:00",
  "warning": -10,
  "id": 1
}
```

## Error Handling

Error responses are not fully specified in the current API specification. Generally, the API follows standard HTTP status codes:

- `200 OK`: The request was successful
- `201 Created`: A new resource was successfully created
- `204 No Content`: The request was successful, but there is no content to return
- `400 Bad Request`: The request was malformed or invalid
- `404 Not Found`: The requested resource was not found
- `500 Internal Server Error`: An error occurred on the server

For more detailed error information, please contact the API provider.
