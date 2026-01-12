# mcp-cimd-sample
CIMDによるMCPでのクライアント認証について検証

## シンプルな認証（ID/PW）

### 手順：サーバー類の起動

#### Step1: 認可サーバーの起動（Start Authorization Server）

```bash
cd ./servers
uv run mcp-simple-auth-as --port=9000
```

#### Step2: リソースサーバー（MCP）の起動 （Start Resource Server (MCP Server)）

```bash
cd ./servers
# Start Resource Server on port 8001, connected to Authorization Server
uv run mcp-simple-auth-rs --port=8001 --auth-server=http://localhost:9000 --transport=streamable-http

# With RFC 8707 strict resource validation (recommended for production)
uv run mcp-simple-auth-rs --port=8001 --auth-server=http://localhost:9000 --transport=streamable-http --oauth-strict
```

#### Step 3: クライアントでの挙動確認（Test with Client）

```bash
cd ./clients
MCP_SERVER_PORT=8001 MCP_TRANSPORT_TYPE=streamable-http uv run mcp-simple-auth-client
```

## XX
