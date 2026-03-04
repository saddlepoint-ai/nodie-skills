# Node: http_request

**Category**: core
**Description**: Make HTTP requests to external APIs. Supports GET/POST/PUT/DELETE with headers, body, and query params. Use for fetching data from REST APIs.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `any` | No | `None` | Credential provider name (e.g., 'github', 'slack', 'product_hunt'). If provided, auth headers will be auto-injected from nodie_vault. |
| `body` | `any` | No | `None` | Request body for POST/PUT/PATCH - any JSON-serializable value |
| `params` | `any` | No | `None` | Query parameters |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `status_code` | `integer` | HTTP status code (e.g., 200, 404, 500) |
| `headers` | `object` | Response headers as key-value pairs (values may be strings or lists) |
| `body` | `any` | Response body (parsed JSON if content-type is application/json, otherwise text) |
| `elapsed_ms` | `number` | Request duration in milliseconds |
