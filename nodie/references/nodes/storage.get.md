# Node: storage.get

**Category**: core
**Description**: Retrieve data from S3, KV storage, or HTTP URL

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `key` | `string` | Yes | `-` | URI to retrieve: s3://path, kv://key, or https://url |
| `as_binary` | `boolean` | No | `False` | Store result in binary context instead of returning content |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `content` | `any` | Retrieved content (None if as_binary=True) |
| `binary_ref` | `any` | Binary reference if as_binary=True |
| `backend` | `string` | Source backend: 's3', 'kv', or 'http' |
| `size` | `integer` | Size in bytes |
| `content_type` | `any` | MIME type of content |
