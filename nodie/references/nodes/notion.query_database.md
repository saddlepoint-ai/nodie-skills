# Node: notion.query_database

**Category**: connector.productivity
**Description**: Query entries from a Notion database

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `notion` | Credential name in vault |
| `database_id` | `string` | Yes | `-` | ID of the Notion database to query |
| `filter` | `any` | No | `None` | Filter conditions for the query |
| `sorts` | `any` | No | `None` | Sort conditions for the query |
| `page_size` | `integer` | No | `100` | Number of results per page (max 100) |
| `start_cursor` | `any` | No | `None` | Cursor for pagination |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `results` | `array` | - |
| `has_more` | `boolean` | - |
| `next_cursor` | `any` | - |
| `total_count` | `integer` | - |
