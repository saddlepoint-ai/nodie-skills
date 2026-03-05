# Node: instagram.full_posts

**Category**: connector.data
**Description**: Search and scrape Instagram hashtags, users, or places

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `apify_system` | Credential: 'apify_system' (system-level) or 'apify' (user-level) |
| `search_type` | `string` | No | `hashtag` | Type of Instagram search: hashtag, user, or place |
| `query` | `any` | No | `None` | Search keyword (required unless direct_urls is provided) |
| `results_type` | `string` | No | `posts` | What to return: 'posts' (post data) or 'details' (metadata/stats) |
| `search_limit` | `integer` | No | `5` | Max number of search results (hashtags/users/places) to return |
| `results_limit` | `integer` | No | `20` | Max posts per search result (only when results_type=posts) |
| `direct_urls` | `any` | No | `None` | Direct Instagram URLs to scrape (bypasses search). Supports profile/post/hashtag/place URLs. |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `items` | `array` | Scraped items from Instagram |
| `total` | `integer` | Number of items returned |
| `search_type` | `any` | Search type used |
| `query` | `any` | Search query used |

