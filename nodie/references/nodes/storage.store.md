# Node: storage.store

**Category**: core
**Description**: Store data to S3 or KV storage with URI-based backend selection

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `content` | `any` | Yes | `-` | Data to store. Can be string, bytes, dict, list, or binary reference |
| `key` | `string` | Yes | `-` | Storage key with optional URI scheme: s3://path, kv://key, or auto-select path |
| `content_type` | `any` | No | `None` | MIME type for S3 storage. Auto-detected if not provided |
| `ttl` | `any` | No | `None` | Time-to-live in seconds (KV storage only) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `url` | `any` | Public URL (S3 storage only) |
| `key` | `string` | Full namespaced storage key |
| `backend` | `string` | Storage backend used: 's3' or 'kv' |
| `size` | `integer` | Size of stored data in bytes |
