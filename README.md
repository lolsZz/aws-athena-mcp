# @lishenxydlgzs/aws-athena-mcp

A Model Context Protocol (MCP) server for running AWS Athena queries. This server enables AI assistants to execute SQL queries against your AWS Athena databases and retrieve results.

## Installation

```bash
npm install -g @lishenxydlgzs/aws-athena-mcp
```

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
      "command": "aws-athena-mcp",
      "args": [],
      "env": {}
    }
  }
}
```

3. The server provides the following tool:

- `run_query`: Execute a SQL query using AWS Athena
  - Parameters:
    - database: The Athena database to query
    - query: SQL query to execute
    - maxRows: Maximum number of rows to return (default: 1000, max: 10000)

## Example

```json
{
  "database": "my_database",
  "query": "SELECT * FROM my_table LIMIT 10",
  "maxRows": 10
}
```

## Requirements

- Node.js >= 16
- AWS credentials with appropriate Athena permissions

## License

MIT

## Repository

[GitHub Repository](https://github.com/lishenxydlgzs/aws-athena-mcp)
