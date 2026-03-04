# Node: rss.read

**Category**: connector.data
**Description**: Fetch and parse RSS/Atom feeds. Returns list of articles with title, link, description, content, published date, and author. Use for news aggregation and content monitoring.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `url` | `string` | Yes | `-` | RSS/Atom feed URL |
| `max_items` | `any` | No | `None` | Maximum number of items to return (default: all) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `title` | `string` | - |
| `link` | `string` | - |
| `description` | `any` | - |
| `content` | `any` | - |
| `published` | `any` | - |
| `author` | `any` | - |
