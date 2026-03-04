# Node: google_drive.create_folder

**Category**: connector.productivity
**Description**: Create a folder in Google Drive

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential: OAuth only (create_folder does not support Service Account) |
| `name` | `string` | Yes | `-` | Folder name |
| `parent_folder_id` | `any` | No | `None` | Parent folder ID |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `folder_id` | `string` | - |
| `name` | `string` | - |
| `web_view_link` | `string` | - |
