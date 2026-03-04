# Node: notion.update_page

**Category**: connector.productivity
**Description**: Update a Notion page's properties

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `notion` | Credential name in vault |
| `page_id` | `string` | Yes | `-` | ID of the Notion page to update |
| `properties` | `any` | No | `None` | Page properties to update |
| `icon` | `any` | No | `None` | Page icon (emoji or URL) |
| `cover` | `any` | No | `None` | Cover image URL |
| `archived` | `any` | No | `None` | Archive or unarchive the page |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `id` | `string` | - |
| `url` | `string` | - |
| `last_edited_time` | `string` | - |
