## Setup Development Environment
Checkout package, install dependencies and build

```bash
cd ${HOME}/workspace
git clone https://github.com/lishenxydlgzs/aws-athena-mcp.git && cd aws-athena-mcp
npm install && npm run build
echo "MCP_PATH: ${HOME}/workspace/aws-athena-mcp/build/index.js"
```

Configure Client

```json
{
  "mcpServers": {
    "aws-athena-mcp": {
      "command": "node",
      "args": [
        "<MCP_PATH>"
      ],
      "env": {
        "OUTPUT_S3_PATH": "s3://<bucket>/<s3_prefix>/",
        "AWS_REGION": "<aws_region>",
        "AWS_PROFILE": "<aws_config_profile>"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

