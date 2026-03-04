# Node: google_drive.get

**Category**: connector.productivity
**Description**: Get file metadata from Google Drive

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential: 'google' (OAuth) or 'google_service_account' (SA, for shareable link) |
| `file_id` | `any` | No | `None` | File ID (alternative to file_url) |
| `file_url` | `any` | No | `None` | Shareable file URL (alternative to file_id) |
| `fields` | `any` | No | `None` | Fields to return (default: all) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `file_id` | `string` | - |
| `name` | `string` | - |
| `mime_type` | `string` | - |
| `size` | `any` | - |
| `created_time` | `string` | - |
| `modified_time` | `string` | - |
| `parents` | `array` | - |
| `web_view_link` | `any` | - |
| `web_content_link` | `any` | - |
