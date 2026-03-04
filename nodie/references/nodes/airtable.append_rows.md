# Node: airtable.append_rows

**Category**: connector.productivity
**Description**: Append rows to an Airtable table

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `airtableTokenApi` | Credential name in vault |
| `base_id` | `string` | Yes | `-` | Airtable Base ID (e.g., 'appXXXXXXXXXXXXXX') |
| `table_name` | `string` | Yes | `-` | Target table name or ID |
| `data` | `array` | Yes | `-` | List of row objects to append. Keys must match Airtable field names. |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `base_id` | `string` | - |
| `table_name` | `string` | - |
| `created_records` | `integer` | - |
| `record_ids` | `array` | - |
