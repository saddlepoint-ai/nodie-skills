# Node: gmail.send

**Category**: connector.messaging
**Description**: Send an email via Gmail

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential name: 'google' (OAuth) or 'google_service_account' (SA) |
| `to` | `any` | Yes | `-` | Recipient email address(es) |
| `subject` | `string` | Yes | `-` | Email subject |
| `body` | `string` | Yes | `-` | Email body content |
| `cc` | `any` | No | `None` | CC recipient(s) |
| `bcc` | `any` | No | `None` | BCC recipient(s) |
| `content_type` | `string` | No | `text` | Content type: 'text' or 'html' |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `message_id` | `string` | - |
| `thread_id` | `string` | - |
| `label_ids` | `array` | - |
