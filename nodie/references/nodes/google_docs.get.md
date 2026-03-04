# Node: google_docs.get

**Category**: connector.productivity
**Description**: Get content from a Google Doc

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential: 'google' (OAuth) or 'google_service_account' (SA, for shareable link) |
| `document_id` | `any` | No | `None` | Document ID (alternative to document_url) |
| `document_url` | `any` | No | `None` | Shareable document URL (alternative to document_id) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `document_id` | `string` | - |
| `title` | `string` | - |
| `content` | `string` | - |
| `revision_id` | `string` | - |
