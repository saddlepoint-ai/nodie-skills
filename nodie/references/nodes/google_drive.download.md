# Node: google_drive.download

**Category**: connector.productivity
**Description**: Download a file from Google Drive

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential: 'google' (OAuth) or 'google_service_account' (SA, for shareable link) |
| `file_id` | `any` | No | `None` | File ID (alternative to file_url) |
| `file_url` | `any` | No | `None` | Shareable file URL (alternative to file_id) |
| `mime_type` | `any` | No | `None` | Export MIME type for Google Workspace documents (e.g., 'application/pdf', 'application/vnd.openxmlformats-officedocument.wordprocessingml.document') |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `file_id` | `string` | - |
| `file_name` | `string` | - |
| `mime_type` | `string` | - |
| `content` | `string` | - |
| `size` | `integer` | - |
