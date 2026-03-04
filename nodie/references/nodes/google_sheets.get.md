# Node: google_sheets.get

**Category**: connector.productivity
**Description**: Get data from a Google Spreadsheet

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential: 'google' (OAuth) or 'google_service_account' (SA, for shareable link) |
| `spreadsheet_id` | `any` | No | `None` | Google Spreadsheet ID (alternative to spreadsheet_url) |
| `spreadsheet_url` | `any` | No | `None` | Shareable spreadsheet URL (alternative to spreadsheet_id) |
| `range` | `string` | Yes | `-` | A1 notation range, e.g., 'Sheet1!A1:D10' or 'Sheet1' for entire sheet |
| `major_dimension` | `string` | No | `ROWS` | How values are grouped: ROWS or COLUMNS |
| `value_render_option` | `string` | No | `FORMATTED_VALUE` | How to render values: FORMATTED_VALUE, UNFORMATTED_VALUE, or FORMULA |
| `include_headers` | `boolean` | No | `True` | If true, first row is treated as headers and values are returned as list of dicts |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `spreadsheet_id` | `string` | - |
| `range` | `string` | - |
| `values` | `array` | - |
| `row_count` | `integer` | - |
| `column_count` | `integer` | - |
