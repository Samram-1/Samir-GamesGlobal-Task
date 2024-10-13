# AWS Serverless Log Management Project

This project implements two serverless functions using AWS Lambda for managing log entries. It includes:

1. **Log Entry Function**: Receives a log entry and saves it to a DynamoDB table.
2. **Get Entries Function**: Retrieves the 100 most recent log entries.

## Project Overview

### Log Entry Format

Each log entry will contain the following fields:
- **ID**: Unique identifier for the log entry.
- **DateTime**: Timestamp for when the log was created.
- **Severity**: Log severity, which can be "info", "warning", or "error".
- **Message**: The actual log message.

### Functionality

- **Function 1**: Exposes an API endpoint to receive log entries and store them in DynamoDB.
- **Function 2**: Exposes an API endpoint that returns the last 100 log entries in JSON format, sorted by the most recent.

## Technology Stack

- **AWS Lambda**: To run code without provisioning or managing servers.
- **DynamoDB**: NoSQL database for storing log entries.
- **AWS SDK**: JavaScript library to interact with AWS services.

## Setup and Deployment

### Step 1: Create a DynamoDB Table

1. Log in to your AWS Management Console.
2. Navigate to **DynamoDB**.
3. Click **Create table**.
4. Set the table name to `LogInfo`.
5. Define the primary key:
   - **ID** (Type: String).
6. Click **Create**.

### Step 2: Create Lambda Functions

#### Function 1: Log Entry Function

1. Navigate to **AWS Lambda** in the console.
2. Click **Create function**.
3. Select **Author from scratch**.
4. Configure the function:
   - Function name: `LogEntry`
   - Runtime: Node.js 18.x (or your preferred version).
5. Click **Create function**.

6. Replace the default code with the code in the two files in this repository. Use the code in the logEntry file to create and lambda function for logging an entry
and the code in the getEntry file for the get entry function.

7. Navigate to API Gateway in the console.

Click Create API.

Choose HTTP API and click Build.

Configure your API:

Name: LogManagementAPI.
Click Next.
Integrate your Lambda functions:

Click Add integration.
Select your LogEntryFunction and click Next.
For the route, set it to /logEntry and method to POST.
Repeat this step for GetEntryFunction and set the route to /getEntry and method to GET.
Click Next to finish creating the API.

Click Deploy and note the API endpoint URLs.

8. Creating a Log Entry
Endpoint: POST {API_ENDPOINT}/logEntry
Request Body:
{
  "Severity": "info",
  "Message": "This is a test log entry"
}
2. Retrieving Log Entries
Endpoint: GET {API_ENDPOINT}/getEntries

You can use the above instruction to test the two functions. 
