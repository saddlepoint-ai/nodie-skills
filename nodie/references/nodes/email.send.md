# Node: email.send

**Category**: connector.messaging
**Description**: Send emails via SMTP. Supports TLS/SSL, authentication, HTML content, and CC/BCC. Use for notifications, newsletters, and alerts.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `any` | No | `smtp` | Credential provider name to use (defaults to 'smtp'). |
| `to` | `string` | Yes | `-` | Recipient email address (comma-separated for multiple) |
| `subject` | `string` | Yes | `-` | Email subject |
| `body` | `string` | Yes | `-` | Email body |
| `content_type` | `string` | No | `text/plain` | Content type: 'text/plain' or 'text/html' |
| `cc` | `any` | No | `None` | CC recipients (comma-separated) |
| `bcc` | `any` | No | `None` | BCC recipients (comma-separated) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `success` | `boolean` | - |
| `message_id` | `any` | - |
| `recipients` | `array` | - |
