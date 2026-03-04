# Node: gmail.get

**Category**: connector.messaging
**Description**: Get email details from Gmail

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential name: 'google' (OAuth) or 'google_service_account' (SA) |
| `message_id` | `string` | Yes | `-` | Message ID |
| `format` | `string` | No | `full` | Format: 'full', 'metadata', 'minimal' |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `message_id` | `string` | - |
| `thread_id` | `string` | - |
| `from` | `string` | - |
| `to` | `string` | - |
| `subject` | `string` | - |
| `date` | `string` | - |
| `snippet` | `string` | - |
| `body` | `string` | - |
| `body_html` | `any` | - |
| `label_ids` | `array` | - |
| `has_attachments` | `boolean` | - |
