# Node: video.fetch

**Category**: connector.data
**Description**: Fetch direct video URL from various platforms (Xiaohongshu, Bilibili, YouTube, etc.)

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `url` | `string` | Yes | `-` | Video page URL (e.g., https://www.xiaohongshu.com/explore/xxx) |
| `timeout` | `integer` | No | `60` | Request timeout in seconds (5-300) |
| `credential` | `string` | No | `apify_system` | Credential: 'apify' (user or system fallback) or 'apify_system' (system-level only) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `video_url` | `string` | Direct URL to the video file (e.g., .mp4) |
| `platform` | `string` | Platform name (e.g., 'xiaohongshu', 'bilibili') |
| `metadata` | `object` | Additional metadata (original_url, etc.) |
