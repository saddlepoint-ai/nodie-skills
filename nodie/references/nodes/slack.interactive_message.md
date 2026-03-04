# Node: slack.interactive_message

**Category**: connector.messaging
**Description**: Send an interactive message with buttons for approval workflows

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `slack` | Credential name in vault (default: 'slack') |
| `channel` | `string` | Yes | `-` | Channel ID or name (e.g., '#approvals' or 'C1234567890') |
| `text` | `string` | Yes | `-` | Fallback text for notifications (required by Slack) |
| `header` | `any` | No | `None` | Header text for the message (displayed prominently) |
| `body` | `any` | No | `None` | Main body text (supports Slack mrkdwn formatting) |
| `actions` | `array` | Yes | `-` | List of action buttons |
| `blocks` | `any` | No | `None` | Custom Block Kit blocks (overrides auto-generated blocks) |
| `timeout_hours` | `any` | No | `48` | Timeout in hours for the approval (default: 48) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `suspend` | `boolean` | Indicates workflow should suspend and wait for callback (returned as _suspend) |
| `suspend_reason` | `string` | Reason for suspension (returned as _suspend_reason) |
| `approval_id` | `string` | Unique identifier for this approval request |
| `channel` | `string` | Channel ID where message was posted |
| `ts` | `string` | Timestamp of the posted message |
| `actions` | `array` | List of action_ids that can trigger callback |
