# Node: google_drive.list

**Category**: connector.productivity
**Description**: List files and folders in Google Drive

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential: 'google' (OAuth) or 'google_service_account' (SA) |
| `query` | `any` | No | `None` | Search query (e.g., 'name contains "report"') |
| `page_size` | `integer` | No | `10` | Maximum number of results (1-1000) |
| `page_token` | `any` | No | `None` | Token for next page |
| `order_by` | `any` | No | `None` | Sort order (e.g., 'name', 'modifiedTime desc') |
| `fields` | `any` | No | `None` | Fields to return (default: nextPageToken, files(id, name, mimeType, size, modifiedTime)) |
| `include_trashed` | `boolean` | No | `False` | Include trashed files |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `files` | `array` | - |
| `count` | `integer` | - |
| `next_page_token` | `any` | - |
