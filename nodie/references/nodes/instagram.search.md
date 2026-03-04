# instagram.search

Search and scrape Instagram data using Apify Instagram Scraper.

## Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| search_type | enum | No | `hashtag` | `hashtag`, `user`, or `place` |
| query | string | Conditional | — | Search keyword (required unless `direct_urls` provided) |
| results_type | enum | No | `posts` | `posts` (post data) or `details` (metadata/stats) |
| search_limit | integer | No | `5` | Max search results (1–100) |
| results_limit | integer | No | `20` | Max posts per result, only when results_type=posts (1–200) |
| direct_urls | string[] | No | — | Direct Instagram URLs to scrape (bypasses search) |
| credential | enum | No | `apify_system` | `apify_system` or `apify` |

## Output

```yaml
items: [...]       # Scraped items from Instagram
total: 42          # Number of items
search_type: "hashtag"
query: "travel"
```

## Examples

### Search hashtag posts
```yaml
- id: ig_hashtag
  type: instagram.search
  params:
    search_type: hashtag
    query: "travel"
    results_type: posts
    search_limit: 5
    results_limit: 20
```

### Search users (metadata only)
```yaml
- id: ig_users
  type: instagram.search
  params:
    search_type: user
    query: "nike"
    results_type: details
    search_limit: 10
```

### Scrape specific URLs
```yaml
- id: ig_direct
  type: instagram.search
  params:
    direct_urls:
      - "https://www.instagram.com/p/ABC123/"
      - "https://www.instagram.com/nike/"
    results_type: posts
```

## Notes

- Uses system-level Apify token by default (no user credential needed)
- Replaces all old `instagram.*` nodes (search_posts, search_user, etc.)
- Old node types still work via backward compatibility mapping
- `direct_urls` accepts profile, post, hashtag, and place URLs
