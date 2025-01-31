# Advanced API Implementation

This project implements a FastAPI-based task management API with versioning, authentication, and proper HTTP exception handling. The API provides the ability to perform CRUD operations (Create, Read, Update, Delete) on tasks, with support for API key-based authentication using environment variables.

## Objectives

- Implement versioning, authentication, and HTTP exception handling.
- Use environment variables to manage API keys.
- Implement appropriate HTTP status codes for various responses:
  - `201` for task creation
  - `204` for task update and deletion
  - `404` for task not found
  - `200` for other cases

## Features

- **Versioning**: The API has two versions, `apiv1` and `apiv2`.
- **Authentication**: API key-based authentication using `.env` for secret management.
- **Task Management**: CRUD operations on tasks.
  - Create a new task
  - Get task details by ID
  - Update task by ID
  - Delete task by ID
- **Exception Handling**: Returns custom error messages and status codes for various cases.

## Installation

### Prerequisites

Ensure that Python 3.7 or higher is installed on your system.

### Step 1: Clone the Repository

```bash
git clone https://github.com/your-username/task-management-api.git
cd task-management-api
```

Step 2: Install Dependencies
Install the required dependencies using pip:

```bash
pip install -r requirements.txt
```
Step 3: Setup Environment Variables
Create a .env file in the root directory of the project with the following content:

```bash
API_KEY=your-secret-api-key
```
Ensure you replace your-secret-api-key with a secure API key. This API key will be required for all API requests.

Note: The .env file should not be committed to version control. Add the .env file to .gitignore to prevent it from being included in the repository.

Step 4: Run the Application
Run the FastAPI app using uvicorn:

```bash
uvicorn main:app --reload
```
The API server will be available at http://127.0.0.1:8000.

API Endpoints
Version 1 (apiv1)
GET /apiv1/tasks/{task_id}
Description: Retrieve the task with the specified task_id.

Parameters:

task_id: The ID of the task to retrieve.
Response: Returns the task details or a 404 error if the task is not found.

Authentication: Requires a valid API key (provided in the request header or as a query parameter).

Example Request:

```bash
GET /apiv1/tasks/1
```
Example Response:
```json
{
  "status": "ok",
  "task": {
    "task_id": 1,
    "task_title": "Laboratory Activity",
    "task_desc": "Create Lab Act 2",
    "is_finished": false
  }
}
POST /apiv1/tasks
```
Description: Create a new task.

Request Body: A JSON object containing task_title, task_desc, and an optional is_finished field (default is false).

Response: Returns the newly created task with a 201 Created status.

Authentication: Requires a valid API key.

Example Request:

```bash
POST /apiv1/tasks
Content-Type: application/json
{
  "task_title": "Finish Lab 4",
  "task_desc": "Complete the lab activity for Task Management"
}
```
Example Response:
```json
{
  "status": "ok",
  "task": {
    "task_id": 2,
    "task_title": "Finish Lab 4",
    "task_desc": "Complete the lab activity for Task Management",
    "is_finished": false
  }
}
PATCH /apiv1/tasks/{task_id}
```
Description: Update a task by task_id.

Request Body: A JSON object with the fields to update (task_title, task_desc, and/or is_finished).

Response: Returns the updated task with a 200 OK status.

Authentication: Requires a valid API key.

Example Request:

```bash
PATCH /apiv1/tasks/1
Content-Type: application/json
{
  "task_title": "Updated Task Title",
  "is_finished": true
}
Example Response:
json
Copy
Edit
{
  "status": "ok",
  "task": {
    "task_id": 1,
    "task_title": "Updated Task Title",
    "task_desc": "Create Lab Act 2",
    "is_finished": true
  }
}
DELETE /apiv1/tasks/{task_id}
```
Description: Delete a task by task_id.

Response: Returns a 204 No Content status if the task is successfully deleted.

Authentication: Requires a valid API key.

Example Request:

```bash
DELETE /apiv1/tasks/1
Example Response:
json
Copy
Edit
{
  "status": "ok"
}
Status Codes
201: Task created successfully.
204: Task updated or deleted successfully, or no tasks available.
404: Task not found.
200: Default status code for successful operations that do not match the specific cases above.
Security
```
API access is secured using an API key, which must be provided either in the request header or as a query parameter. The API key is managed securely through an .env file. Ensure you do not share the .env file publicly.
