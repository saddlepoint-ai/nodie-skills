# Node: google_drive.upload

**Category**: connector.productivity
**Description**: Upload a file to Google Drive

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential: OAuth only (upload does not support Service Account) |
| `name` | `string` | Yes | `-` | File name |
| `content` | `string` | Yes | `-` | File content (base64 encoded or raw string) |
| `parent_folder_id` | `any` | No | `None` | Parent folder ID |
| `mime_type` | `any` | No | `None` | MIME type (auto-detected from name if not provided) |
| `is_base64` | `boolean` | No | `False` | Set to true if content is base64 encoded |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `file_id` | `string` | - |
| `name` | `string` | - |
| `mime_type` | `string` | - |
| `size` | `string` | - |
| `web_view_link` | `string` | - |
