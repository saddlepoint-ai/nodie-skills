# Node: google_sheets.create

**Category**: connector.productivity
**Description**: Create a new Google Spreadsheet

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential: OAuth only (create does not support Service Account) |
| `title` | `string` | Yes | `-` | Spreadsheet title |
| `sheet_names` | `any` | No | `None` | List of sheet names to create. Defaults to ['Sheet1'] if not provided. |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `spreadsheet_id` | `string` | - |
| `title` | `string` | - |
| `spreadsheet_url` | `string` | - |
| `sheets` | `array` | - |
