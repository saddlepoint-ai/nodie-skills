# Node: google_sheets.append_rows

**Category**: connector.productivity
**Description**: Append rows to a Google Sheet

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential: 'google' (OAuth) or 'google_service_account' (SA, for shareable link) |
| `spreadsheet_id` | `any` | No | `None` | Google Spreadsheet ID (alternative to spreadsheet_url) |
| `spreadsheet_url` | `any` | No | `None` | Shareable spreadsheet URL (alternative to spreadsheet_id) |
| `sheet_name` | `string` | No | `Sheet1` | Target sheet name |
| `data` | `array` | Yes | `-` | List of row objects to append. Keys become column headers. |
| `value_input_option` | `string` | No | `USER_ENTERED` | How to interpret input: USER_ENTERED or RAW |
| `insert_data_option` | `string` | No | `INSERT_ROWS` | How to insert: INSERT_ROWS or OVERWRITE |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `spreadsheet_id` | `string` | - |
| `updated_range` | `string` | - |
| `updated_rows` | `integer` | - |
| `updated_cells` | `integer` | - |
