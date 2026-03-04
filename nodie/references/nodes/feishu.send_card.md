# Node: feishu.send_card

**Category**: connector.messaging
**Description**: Send messages or interactive cards to Feishu (飞书)

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `feishu` | Credential name in vault (must have app_id and app_secret) |
| `receive_id_type` | `string` | No | `open_id` | The type of receive_id (open_id, user_id, union_id, email, chat_id) |
| `receive_id` | `string` | Yes | `-` | The ID of the receiver (user or chat) |
| `msg_type` | `string` | No | `interactive` | Message type: interactive (card), text, post, etc. |
| `content` | `any` | Yes | `-` | Message content. For 'interactive', this is the card JSON. |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `message_id` | `string` | The ID of the sent message |
| `status` | `string` | - |
