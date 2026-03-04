# Node: notion.create_page

**Category**: connector.productivity
**Description**: Create a page in a Notion database

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `notion` | Credential name in vault |
| `database_id` | `string` | Yes | `-` | ID of the Notion database to add the page to |
| `properties` | `object` | Yes | `-` | Page properties matching database schema |
| `content` | `any` | No | `None` | Page content as markdown |
| `icon` | `any` | No | `None` | Page icon (emoji or URL) |
| `cover` | `any` | No | `None` | Cover image URL |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `id` | `string` | - |
| `url` | `string` | - |
| `created_time` | `string` | - |
