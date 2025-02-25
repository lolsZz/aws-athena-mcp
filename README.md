# @lishenxydlgzs/aws-athena-mcp

A Model Context Protocol (MCP) server for running AWS Athena queries. This server enables AI assistants to execute SQL queries against your AWS Athena databases and retrieve results.

## Usage

1. Configure AWS credentials using one of the following methods:
   - AWS CLI configuration
   - Environment variables (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY)
   - IAM role (if running on AWS)

2. Add the server to your MCP configuration:

```json
{
  "mcpServers": {
    "athena": {
      "command": "npx",
      "args": ["-y", "@lishenxydlgzs/aws-athena-mcp"],
      "env": {
        // Required
        "OUTPUT_S3_PATH": "s3://your-bucket/athena-results/",
        
        // Optional AWS configuration
        "AWS_REGION": "us-east-1",                    // Default: AWS CLI default region
        "AWS_PROFILE": "default",                     // Default: 'default' profile
        "AWS_ACCESS_KEY_ID": "",                      // Optional: AWS access key
        "AWS_SECRET_ACCESS_KEY": "",                  // Optional: AWS secret key
        "AWS_SESSION_TOKEN": "",                      // Optional: AWS session token
        
        // Optional server configuration
        "QUERY_TIMEOUT_MS": "300000",                // Default: 5 minutes (300000ms)
        "MAX_RETRIES": "100",                        // Default: 100 attempts
        "RETRY_DELAY_MS": "500"                      // Default: 500ms between retries
      }
    }
  }
}
```

3. The server provides the following tools:

- `run_query`: Execute a SQL query using AWS Athena
  - Parameters:
    - database: The Athena database to query
    - query: SQL query to execute
    - maxRows: Maximum number of rows to return (default: 1000, max: 10000)
  - Returns:
    - If query completes within timeout: Full query results
    - If timeout reached: Only the queryExecutionId for later retrieval

- `get_status`: Check the status of a query execution
  - Parameters:
    - queryExecutionId: The ID returned from run_query
  - Returns:
    - state: Query state (QUEUED, RUNNING, SUCCEEDED, FAILED, or CANCELLED)
    - stateChangeReason: Reason for state change (if any)
    - submissionDateTime: When the query was submitted
    - completionDateTime: When the query completed (if finished)
    - statistics: Query execution statistics (if available)

- `get_result`: Retrieve results for a completed query
  - Parameters:
    - queryExecutionId: The ID returned from run_query
    - maxRows: Maximum number of rows to return (default: 1000, max: 10000)
  - Returns:
    - Full query results if the query has completed successfully
    - Error if query failed or is still running

## Examples

Running a query:
```json
{
  "database": "my_database",
  "query": "SELECT * FROM my_table LIMIT 10",
  "maxRows": 10
}
```

Checking query status:
```json
{
  "queryExecutionId": "12345-67890-abcdef"
}
```

Getting results for a completed query:
```json
{
  "queryExecutionId": "12345-67890-abcdef",
  "maxRows": 10
}
```

## Requirements

- Node.js >= 16
- AWS credentials with appropriate Athena permissions
- S3 bucket for query results

## License

MIT

## Repository

[GitHub Repository](https://github.com/lishenxydlgzs/aws-athena-mcp)
