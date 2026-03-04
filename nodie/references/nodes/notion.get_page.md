# Node: notion.get_page

**Category**: connector.productivity
**Description**: Get a Notion page by ID

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `notion` | Credential name in vault |
| `page_id` | `string` | Yes | `-` | ID of the Notion page to retrieve |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `id` | `string` | - |
| `url` | `string` | - |
| `created_time` | `string` | - |
| `last_edited_time` | `string` | - |
| `properties` | `object` | - |
