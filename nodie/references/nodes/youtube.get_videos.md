# Node: youtube.get_videos

**Category**: connector.data
**Description**: Get detailed information about YouTube videos using Apify

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `apify_system` | Credential: 'apify' (user or system fallback) or 'apify_system' (system-level only) |
| `video_ids` | `any` | Yes | `-` | Video ID(s) or URLs to retrieve (list or comma-separated string) |
| `timeout_secs` | `integer` | No | `300` | Timeout in seconds for the operation |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `videos` | `array` | Video details |
| `count` | `integer` | Number of videos returned |
