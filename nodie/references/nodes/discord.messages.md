# Node: discord.messages

**Category**: connector.data
**Description**: Read messages from a Discord channel

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `channel_id` | `string` | Yes | `-` | Discord channel ID to read messages from |
| `limit` | `integer` | No | `100` | Number of messages to fetch (default: 100, max: 500) |
| `keyword` | `any` | No | `None` | Optional keyword to filter messages (case-insensitive) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `messages` | `array` | List of message objects |
| `total` | `integer` | Number of messages returned |
