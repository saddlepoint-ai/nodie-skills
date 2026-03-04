# Node: youtube.get_channel

**Category**: connector.data
**Description**: Get information about a YouTube channel using Apify

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `apify_system` | Credential: 'apify' (user or system fallback) or 'apify_system' (system-level only) |
| `channel_id` | `any` | No | `None` | Channel ID or URL to retrieve |
| `for_handle` | `any` | No | `None` | Channel handle (e.g., @username) |
| `timeout_secs` | `integer` | No | `300` | Timeout in seconds for the operation |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `channel` | `any` | Channel details |
| `found` | `boolean` | Whether channel was found |
