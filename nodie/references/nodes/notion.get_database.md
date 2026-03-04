# Node: notion.get_database

**Category**: connector.productivity
**Description**: Get a Notion database schema and metadata

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `notion` | Credential name in vault |
| `database_id` | `string` | Yes | `-` | ID of the Notion database to retrieve |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `id` | `string` | - |
| `title` | `string` | - |
| `description` | `string` | - |
| `url` | `string` | - |
| `properties` | `object` | - |
| `created_time` | `string` | - |
| `last_edited_time` | `string` | - |
