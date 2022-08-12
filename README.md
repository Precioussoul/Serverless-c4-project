# Serverless TODO Application Project

This is the project four of udacity cloud developer nanodegree program and this is the capstone project to graduation. In this project, I implemented a simple TODO application using AWS Lambda and Serverless framework.

# Functionality of the application

This application allow user to create/remove/update/fetch TODO items. Each TODO item can optionally have an attachment image. Each user only has access to TODO items that he/she has created.

# TODO items

The application should store TODO items, and each TODO item contains the following fields:

- `todoId` (string) - a unique id for an item
- `createdAt` (string) - date and time when an item was created
- `name` (string) - name of a TODO item (e.g. "Change a light bulb")
- `dueDate` (string) - date and time by which an item should be completed
- `done` (boolean) - true if an item was completed, false otherwise
- `attachmentUrl` (string) (optional) - a URL pointing to an image attached to a TODO item

You might also store an id of a user who created a TODO item.

## Prerequisites

- <a href="https://manage.auth0.com/" target="_blank">Auth0 account</a>
- <a href="https://github.com" target="_blank">GitHub account</a>
- <a href="https://nodejs.org/en/download/package-manager/" target="_blank">NodeJS</a> version up to 12.xx
- Serverless
  - Create a <a href="https://dashboard.serverless.com/" target="_blank">Serverless account</a> user
  - Install the Serverless Framework’s CLI (up to VERSION=2.21.1). Refer to the <a href="https://www.serverless.com/framework/docs/getting-started/" target="_blank">official documentation</a> for more help.
  ```bash
  npm install -g serverless
  serverless --version
  ```
  - Login and configure serverless to use the AWS credentials
  ```bash
  # Login to your dashboard from the CLI. It will ask to open your browser and finish the process.
  serverless login
  # Configure serverless to use the AWS credentials to deploy the application
  # You need to have a pair of Access key (YOUR_ACCESS_KEY_ID and YOUR_SECRET_KEY) of an IAM user with Admin access permissions
  serverless config credentials --provider aws --key YOUR_ACCESS_KEY_ID --secret YOUR_SECRET_KEY --profile serverless
  ```

# Functions implemented

In this project, the following functions and configured in the `serverless.yml` file:

- Authorizer function
- GetuploadURL function
- CreateTodoItem function
- DeleteTodoItem function
- UpdateTodoItem function

- `Auth` - this function should implement a custom authorizer for API Gateway that should be added to all other functions.

- `GetTodos` - should return all TODOs for a current user. A user id can be extracted from a JWT token that is sent by the frontend

- `CreateTodo` - should create a new TODO for a current user. A shape of data send by a client application to this function can be found in the `CreateTodoRequest.ts` file

It receives a new TODO item to be created in JSON format that looks like this:

- `UpdateTodo` - should update a TODO item created by a current user. A shape of data send by a client application to this function can be found in the `UpdateTodoRequest.ts` file

The id of an item that should be updated is passed as a URL parameter.

It should return an empty body.

- `DeleteTodo` - should delete a TODO item created by a current user. Expects an id of a TODO item to remove.

It returned an empty body.

- `GenerateUploadUrl` - returns a pre-signed URL that can be used to upload an attachment file for a TODO item.

All functions are already connected to appropriate events from API Gateway.

An id of a user can be extracted from a JWT token passed by a client.

You also need to add any necessary resources to the `resources` section of the `serverless.yml` file such as DynamoDB table and S3 bucket.

# How to run the application

## Backend

To deploy an application run the following commands:

```
cd backend
npm install
sls deploy -v
```

## Frontend

To run a client application first edit the `client/src/config.ts` file to set correct parameters. And then run the following commands:

```
cd client
npm install
npm run start
```

This should start a development server with the React application that will interact with the serverless TODO application.
