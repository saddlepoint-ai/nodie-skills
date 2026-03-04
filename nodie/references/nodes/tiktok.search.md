# tiktok.search

Search TikTok by keyword or scrape from profile/hashtag/music/location URLs using Apify.

## Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| query | string | Conditional | — | Search keyword. Required if `start_urls` is not set. |
| start_urls | string[] | Conditional | — | TikTok URLs to scrape (profile, hashtag, search, music, location). Overrides `query` if set. |
| max_items | integer | No | `15` | Maximum posts to return (10–500; actor requires at least 10 per run) |
| location | string | No | — | ISO 3166-1 alpha-2 country code to filter results by region (e.g., `US`, `GB`) |
| credential | enum | No | `apify_system` | `apify_system` or `apify` |

## Output

```yaml
items: [...]        # Scraped TikTok posts (id, title, views, likes, channel, video, etc.)
total: 42           # Number of items
query: "travel"     # Search query used
```

## Examples

### Search by keyword
```yaml
- id: tiktok_search
  type: tiktok.search
  params:
    query: "trending products"
    max_items: 20
    location: US
```

### Scrape a hashtag page
```yaml
- id: tiktok_hashtag
  type: tiktok.search
  params:
    start_urls:
      - "https://www.tiktok.com/tag/giftideas"
    max_items: 30
```

### Scrape a profile
```yaml
- id: tiktok_profile
  type: tiktok.search
  params:
    start_urls:
      - "https://www.tiktok.com/@someuser"
    max_items: 15
```

## Notes

- Uses system-level Apify token by default (no user credential needed)
- Actor: `apidojo/tiktok-scraper` — pricing ~$0.30 / 1,000 posts
- `max_items` minimum is 10 (actor constraint)
- `start_urls` accepts profile, hashtag, search, music, and location URLs
