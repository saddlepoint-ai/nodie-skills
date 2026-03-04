# Node: trello.create_card

**Category**: connector.productivity
**Description**: Create a card in a Trello board

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `trello` | Credential name in vault |
| `list_id` | `string` | Yes | `-` | ID of the Trello list to add the card to |
| `name` | `string` | Yes | `-` | Card title |
| `desc` | `any` | No | `None` | Card description (supports Markdown) |
| `pos` | `string` | No | `bottom` | Position in list: 'top', 'bottom', or positive number |
| `due` | `any` | No | `None` | Due date in ISO 8601 format |
| `labels` | `any` | No | `None` | List of label IDs to attach |
| `members` | `any` | No | `None` | List of member IDs to assign |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `id` | `string` | - |
| `name` | `string` | - |
| `short_url` | `string` | - |
| `url` | `string` | - |
| `list_id` | `string` | - |
| `board_id` | `string` | - |
