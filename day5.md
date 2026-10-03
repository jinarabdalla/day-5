Exercise A: User Manual Procedure
Title: Creating a Python Virtual Environment and Installing a Package
This guide will walk you through creating an isolated Python Virtual Environment and installing an external software package using the command line interface.

Prerequisites
Before starting, ensure you have the following ready:
A computer running Windows, macOS, or Linux.
Python 3.3 or higher installed on your system.
An active Internet connection to download packages.
Basic familiarity with opening your operating system's terminal application (Command Prompt or PowerShell on Windows; Terminal on macOS and Linux).

Step-by-Step Procedure
Open your command line application.
Action: Open Command Prompt (Windows) or Terminal (macOS/Linux).
Expected Result: A window appears with a text prompt showing your current directory path followed by a blinking cursor.
Navigate to your workspace directory.
Action: Type cd Desktop and press Enter.
Expected Result: The directory path in your prompt updates to show that you are now working inside your Desktop folder.
Create a new project directory.
Action: Type mkdir python_project and press Enter.
Expected Result: A new folder named python_project is silently created on your Desktop.
Navigate into your new project directory.
Action: Type cd python_project and press Enter.
Expected Result: The command prompt updates to show you are inside the python_project directory.
Generate the virtual environment.
Action: Type python -m venv myenv and press Enter.
Expected Result: The prompt freezes momentarily, then returns to a blank line. A new folder named myenv is successfully created inside your project directory.
Activate the virtual environment.
Action: Type the activation command matching your operating system and press Enter:
Windows (Command Prompt): myenv\Scripts\activate
macOS / Linux: source myenv/bin/activate
Expected Result: The terminal prompt updates to display (myenv) at the very beginning of the line, indicating the environment is now active.
Verify that the environment is isolated.
Action: Type pip list and press Enter.
Expected Result: A short table prints out displaying only two default base packages: pip and setuptools.
Install an external package.
Action: Type pip install requests and press Enter.
Expected Result: Text scrolls down the screen showing download progress bars, concluding with a successful message like Successfully installed requests-....

Screenshot Description
Location in text: Place immediately after Step 6 (Activate the virtual environment).
Visual Contents: A screenshot of a terminal window. The top lines show the execution of the python -m venv myenv command. Below that, the activation command (source myenv/bin/activate or myenv\Scripts\activate) is visible. The central focus of the screenshot must be a red circle or arrow highlighting the (myenv) prefix at the beginning of the newest prompt line, proving the environment is active.

Troubleshooting Note
Common Error: "python" or "pip" is not recognized as an internal or external command (or command not found: python).
Cause: This happens because your operating system cannot find the Python executable framework. It means Python is either not installed, or its installation path was not added to your system's environmental variables (PATH) during installation.
Solution: Re-run your original Python installer file. Look closely at the very first window that pops up, check the box that says "Add python.exe to PATH", and click "Install Now". Restart your terminal application and try the steps again.

Exercise B: API Reference Entry
Create Task Endpoint
Endpoint Definition
HTTP Method: POST
Path: /api/v1/projects/{projectId}/tasks

Description
Creates a brand new task within a specified project. The authenticating user must have explicit "write" or "editor" access permissions inside the project container to perform this act
Headers
Header Name
Type
Required
Description
Content-Type
String
Yes
Must be set exactly to application/json.
Authorization
String
Yes
Bearer token format for authentication. Example: Bearer <your_jwt_token>.


Request Parameters
Path Parameters
Parameter Name
Data Type
Required
Description
projectId
String (UUID)
Yes
The unique identifier of the project where this task will belong.

Body Parameters
Parameter Name
Data Type
Required
Description
title
String
Yes
The summary or name of the task. Max length: 255 characters.
description
String
No
Detailed explanation of the task work items.
assigneeId
String (UUID)
Yes
The unique user ID of the team member assigned to execute this task.
dueDate
String (ISO 8601)
Yes
The target completion date formatted as YYYY-MM-DD.
priority
String
Yes
The urgency designation. Must be exactly one of: low, medium, or high.


HTTP Response Codes
Status Code
Status Meaning
Trigger Condition
201 Created
Created
The task was successfully validated, generated, and saved to the database.
400 Bad Request
Bad Request
Missing a required body field, an invalid date format, or an unrecognized value for priority.
401 Unauthorized
Unauthorized
The request is missing a valid Authorization header, or the provided token is expired.
403 Forbidden
Forbidden
The authenticated user is recognized but does not have permission to modify this specific project.
404 Not Found
Not Found
The projectId provided in the URL path does not match any existing project record.


Example JSON Request Body
json
{
  "title": "Implement User Authentication Flow",
  "description": "Set up JWT-based authorization, login endpoints, and secure middleware routes.",
  "assigneeId": "8f3b2a19-c4d5-4e6f-8a7b-9c0d1e2f3a4b",
  "dueDate": "2026-10-15",
  "priority": "high"
}

Use code with caution.

Example JSON Successful Response Body (201 Created)
json
{
  "id": "5e1a2b3c-4d5e-6f7a-8b9c-0d1e2f3a4b5c",
  "projectId": "1a2b3c4d-5e6f-7a8b-9c0d-1e2f3a4b5c6d",
  "title": "Implement User Authentication Flow",
  "description": "Set up JWT-based authorization, login endpoints, and secure middleware routes.",
  "assigneeId": "8f3b2a19-c4d5-4e6f-8a7b-9c0d1e2f3a4b",
  "dueDate": "2026-10-15",
  "priority": "high",
  "status": "todo",
  "creatorId": "3b2a198f-d5c4-6f4e-7b8a-2f3a4b9c0d1e",
  "createdAt": "2026-10-03T12:43:00Z",
  "updatedAt": "2026-10-03T12:43:00Z"
vv
