# Node: twitter.search

**Category**: connector.data
**Description**: Search Twitter (X) tweets by keyword or user

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `apify_system` | Credential: 'apify' (user or system fallback) or 'apify_system' (system-level only) |
| `query` | `string` | Yes | `-` | Search keyword or username (e.g., 'AI automation' or 'elonmusk') |
| `search_type` | `string` | No | `keyword` | Search type: keyword (search tweets) or user (get user tweets) |
| `max_items` | `integer` | No | `25` | Maximum number of tweets to return (1-500) |
| `sort_by` | `string` | No | `Top` | Sort order: Top (most popular) or Latest (newest first) |
| `lang` | `any` | No | `en` | Language code filter (e.g., 'en', 'zh', 'ja', 'es') |
| `since_date` | `any` | No | `None` | Start date filter (YYYY-MM-DD format) |
| `until_date` | `any` | No | `None` | End date filter (YYYY-MM-DD format) |
| `min_likes` | `any` | No | `5` | Minimum number of likes |
| `min_retweets` | `any` | No | `None` | Minimum number of retweets |
| `min_replies` | `any` | No | `None` | Minimum number of replies |
| `has_media` | `any` | No | `None` | Filter tweets that contain media (images/videos) |
| `verified_only` | `any` | No | `None` | Only return tweets from verified accounts |
| `exclude_replies` | `boolean` | No | `True` | Exclude replies to other tweets |
| `exclude_links_only` | `boolean` | No | `True` | Exclude tweets that only contain links without text content |
| `min_text_length` | `integer` | No | `20` | Minimum tweet text length to filter out too short content |
| `min_author_followers` | `any` | No | `None` | Minimum number of followers for the author |
| `timeout_secs` | `integer` | No | `300` | Timeout in seconds for the search operation |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `tweets` | `array` | List of tweet objects |
| `total` | `integer` | Number of tweets returned |
