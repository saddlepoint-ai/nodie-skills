# Node: xhs.get_comments

**Category**: connector.data
**Description**: Scrape actual comment content from Xiaohongshu posts via comment_v2_sync. Uses system env XHS_APP_API_KEY. REQUIRED for sentiment/reputation analysis. Use after xhs.search to get comments from high-engagement notes. Returns full comment text, user info, likes, and nested replies.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `post_urls` | `array` | Yes | `-` | List of Xiaohongshu post URLs or note IDs |
| `max_pages` | `any` | No | `3` | Maximum pages to collect (null to fetch all) |
| `sort_strategy` | `any` | No | `` | Sort strategy: ''=default, latest_v2=latest, like_count=most likes |
| `timeout_secs` | `integer` | No | `300` | Timeout in seconds for the operation |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `comments` | `array` | List of comment objects with nested replies |
| `total` | `integer` | Number of comments returned |

## Common Mistakes

Do NOT use upstream/raw XHS API parameter names not listed in this schema. Use ONLY the parameters listed in the table above: `post_urls`, `max_pages`, `sort_strategy`, `timeout_secs`.
