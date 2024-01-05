# Azure Logic App Project

This repository contains Azure Logic App workflows designed to interact with the Reed job API. The Logic App workflows are categorized into different types: Stateless and Stateful.

## Workflows

### 1. Stateless Workflow

#### Trigger: Manual HTTP Request

- **Description:** This workflow fetches job details from the Reed API based on the provided job ID.
- **Trigger Type:** Manual HTTP Request
- **Trigger Method:** GET
- **Endpoint:** `/jobs/{ID}`
- **Authentication:** Basic Authentication
  - Username: `f3640f5f-3cc9-4daf-aa3d-5e0c28235262`
  - Password: [your-password-here]

#### Actions:

1. **HTTP Action (Job Details):**
   - Method: GET
   - URI: `https://www.reed.co.uk/api/1.0/jobs/@{triggerOutputs()['queries']['ID']}`
   - Authentication: Basic Authentication
     - Username: `f3640f5f-3cc9-4daf-aa3d-5e0c28235262`

2. **Response Action:**
   - Body: `@body('HTTP')`
   - Status Code: 200
   - Triggered After: HTTP Action (Job Details) Succeeded

### 2. Stateful Workflow

#### Trigger: Manual HTTP Request

- **Description:** This workflow performs a job search using keywords provided in the request body.
- **Trigger Type:** Manual HTTP Request
- **Trigger Method:** GET
- **Endpoint:** `/search`
- **Authentication:** Basic Authentication
  - Username: `f3640f5f-3cc9-4daf-aa3d-5e0c28235262`
  - Password: [your-password-here]

#### Actions:

1. **HTTP Action (Job Search):**
   - Method: GET
   - URI: `https://www.reed.co.uk/api/1.0/search?`
   - Authentication: Basic Authentication
     - Username: `f3640f5f-3cc9-4daf-aa3d-5e0c28235262`
   - Queries: `keywords`: `@{triggerBody()['keywords']}`

2. **Response Action:**
   - Body: `@body('HTTP')`
   - Status Code: 200
   - Triggered After: HTTP Action (Job Search) Succeeded

### 3. Stateless Workflow with Parameters

#### Trigger: Manual HTTP Request

- **Description:** This workflow performs a job search using a dynamic username provided as a parameter.
- **Trigger Type:** Manual HTTP Request
- **Trigger Method:** GET
- **Endpoint:** `/search`

#### Actions:

1. **HTTP Action (Job Search):**
   - Method: GET
   - URI: `https://www.reed.co.uk/api/1.0/search?`
   - Authentication: Basic Authentication
     - Username: `@parameters('Username')`
     - Password: [your-password-here]

2. **Response Action:**
   - Body: `@body('HTTP')`
   - Status Code: 200
   - Triggered After: HTTP Action (Job Search) Succeeded

## How to Use

1. Clone this repository.
2. Import the Logic App workflows into your Azure environment.
3. Configure the necessary parameters, such as API credentials.
4. Trigger the workflows manually or integrate them into your applications.

Feel free to customize and extend these workflows based on your specific requirements.
