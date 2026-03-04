# Node: feishu.bitable_append

**Category**: connector.productivity
**Description**: Append a record to a Feishu Bitable (飞书多维表格)

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `feishu` | Credential name in vault |
| `app_token` | `string` | Yes | `-` | The token of the Bitable app |
| `table_id` | `string` | Yes | `-` | The ID of the table |
| `fields` | `object` | Yes | `-` | The fields to append as a new record |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `record_id` | `string` | The ID of the created record |
| `status` | `string` | - |
