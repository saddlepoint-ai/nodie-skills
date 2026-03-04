# pinterest.search

Search Pinterest pins by keyword using Apify.

## Parameters

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| query | string | Conditional | — | Search keyword. Required if `search_queries` is not set. |
| search_queries | string[] | Conditional | — | Multiple search keywords. Overrides `query` if set. |
| max_results | integer | No | `25` | Maximum pins per query (1–250) |
| include_comments | boolean | No | `false` | Fetch comments for each pin |
| max_comments | integer | No | — | Max comments per pin when `include_comments=true` (1–100) |
| max_total_charge_usd | float | No | — | Optional spending cap per run (USD) |
| credential | enum | No | `apify_system` | `apify_system` or `apify` |

## Output

```yaml
items: [...]      # Scraped pins (id, url, title, images, saves, pinner, board, etc.)
total: 42         # Number of items
query: "travel"   # Primary search query used (null when search_queries used)
```

## Examples

### Search by keyword
```yaml
- id: pinterest_search
  type: pinterest.search
  params:
    query: "trending LA gifts"
    max_results: 30
```

### Search multiple keywords
```yaml
- id: pinterest_multi
  type: pinterest.search
  params:
    search_queries:
      - "gift shop LA"
      - "trending home decor"
    max_results: 25
```

### Search with comments
```yaml
- id: pinterest_with_comments
  type: pinterest.search
  params:
    query: "minimalist office"
    max_results: 20
    include_comments: true
    max_comments: 10
```

## Notes

- Uses system-level Apify token by default (no user credential needed)
- Actor: `devcake/pinterest-search-scraper` — pricing ~$4 / 1,000 results
- Returns 40+ fields per pin including saves, likes, comments, pinner, and board info
- Use `max_total_charge_usd` to cap spending on large keyword sets
