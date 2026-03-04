# Node: reddit.search

**Category**: connector.data
**Description**: Search Reddit posts, subreddits, or users

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `apify_system` | Credential: 'apify' (user or system fallback) or 'apify_system' (system-level only) |
| `query` | `string` | Yes | `-` | Search keyword, subreddit name, user name, or post URL |
| `search_type` | `string` | No | `search` | Scraping type: search (keyword), subreddit, user, or single post |
| `max_items` | `integer` | No | `25` | Maximum number of items to return (1-1000) |
| `sort` | `string` | No | `relevance` | Sort order for results |
| `time_filter` | `string` | No | `all` | Time range filter |
| `include_comments` | `boolean` | No | `False` | Whether to include comments in the results |
| `timeout_secs` | `integer` | No | `300` | Timeout in seconds for the search operation |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `posts` | `array` | List of post objects |
| `total` | `integer` | Number of posts returned |
