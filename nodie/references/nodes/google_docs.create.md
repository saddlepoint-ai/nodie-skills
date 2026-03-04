# Node: google_docs.create

**Category**: connector.productivity
**Description**: Create a new Google Doc

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential: OAuth only (create does not support Service Account) |
| `title` | `string` | Yes | `-` | Document title |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `document_id` | `string` | - |
| `title` | `string` | - |
| `document_link` | `string` | - |
