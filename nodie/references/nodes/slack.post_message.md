# Node: slack.post_message

**Category**: connector.messaging
**Description**: Post a message to a Slack channel

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `slack` | Credential name in vault (default: 'slack') |
| `channel` | `string` | Yes | `-` | Channel ID or name (e.g., '#general' or 'C1234567890') |
| `text` | `string` | Yes | `-` | Message text (supports Slack mrkdwn formatting) |
| `blocks` | `any` | No | `None` | Block Kit blocks for rich message formatting |
| `thread_ts` | `any` | No | `None` | Thread timestamp to reply to (creates threaded message) |
| `unfurl_links` | `boolean` | No | `True` | Enable/disable URL previews |
| `unfurl_media` | `boolean` | No | `True` | Enable/disable media previews |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `ok` | `boolean` | Whether the API call was successful |
| `channel` | `string` | Channel ID where message was posted |
| `ts` | `string` | Timestamp of the posted message |
| `message` | `object` | Posted message object |
