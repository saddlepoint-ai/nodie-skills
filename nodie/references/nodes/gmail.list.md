# Node: gmail.list

**Category**: connector.messaging
**Description**: List emails from Gmail

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential name: 'google' (OAuth) or 'google_service_account' (SA) |
| `query` | `any` | No | `None` | Search query (e.g., 'is:unread from:boss') |
| `label_ids` | `any` | No | `None` | Filter by label IDs (e.g., ['INBOX']) |
| `max_results` | `integer` | No | `10` | Max number of results (1-100) |
| `include_spam_trash` | `boolean` | No | `False` | Include messages from SPAM and TRASH |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `messages` | `array` | - |
| `count` | `integer` | - |
| `next_page_token` | `any` | - |
