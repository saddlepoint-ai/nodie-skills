# Node: youtube.search

**Category**: connector.data
**Description**: Search YouTube for videos, channels, or playlists using Apify

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `apify_system` | Credential: 'apify' (user or system fallback) or 'apify_system' (system-level only) |
| `query` | `string` | Yes | `-` | Search query string |
| `max_results` | `integer` | No | `10` | Maximum number of results to return (1-100) |
| `sort_order` | `any` | No | `relevance` | Sort order for search results |
| `date_filter` | `any` | No | `None` | Filter results by upload date |
| `timeout_secs` | `integer` | No | `300` | Timeout in seconds for the search operation |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `items` | `array` | Search results |
| `total_results` | `integer` | Total number of results returned |
| `video_ids` | `array` | List of video IDs (convenience field) |
