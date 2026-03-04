# Node: xhs.search

**Category**: connector.data
**Description**: Search Xiaohongshu (RedNote) notes by keyword via search_v2_sync. Uses system env XHS_APP_API_KEY. Returns note metadata and engagement COUNTS only, NOT actual comment content. For sentiment/comment analysis, use xhs.get_comments.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `keywords` | `any` | Yes | `-` | Search keywords (string or list of strings) |
| `max_items` | `integer` | No | `20` | Maximum number of notes to return (1-100). Used to cap output. |
| `sort_by` | `string` | No | `general` | Sort order for search_v2_sync (supports general/time/popularity/comment/collect) |
| `note_type` | `string` | No | `all` | Filter by note type (mapped to search_v2_sync filter_note_type) |
| `time_filter` | `any` | No | `None` | Time filter for search_v2_sync |
| `timeout_secs` | `integer` | No | `300` | Timeout in seconds for the search operation |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `notes` | `array` | List of note objects (see Note Object Fields below) |
| `total` | `integer` | Number of notes returned |

### Note Object Fields

Each note object in the `notes` array contains:

| Field | Type | Description |
|-------|------|-------------|
| `note_id` | `string` | Unique note identifier |
| `title` | `string` | Note title |
| `description` | `string` | Note description/content |
| `url` | `string` | Basic URL format: `https://www.xiaohongshu.com/explore/{note_id}` |
| `link` | `string` | Full URL with `xsec_token` parameter for direct access (if available from API). Format: `https://www.xiaohongshu.com/explore/{note_id}?xsec_token={token}`. Use this field for direct links to notes. |
| `author` | `object` | Author information: `nickname`, `user_id`, `red_id` |
| `engagement` | `object` | Engagement metrics: `likes`, `collects`, `comments`, `shares` |
| `cover_image` | `string` | Cover image URL |
| `type` | `string` | Note type |
| `created_at` | `string` | Creation timestamp |
| `raw` | `object` | Raw API response data |

## Common Mistakes

Do NOT use upstream/raw XHS API parameter names not listed in this schema. Common incorrect parameters to avoid:
- `page`, `page_size`, `keyword` (singular), `sort`, `search_id` — these are from the raw XHS API, not the Nodie node.
- Use ONLY the parameters listed in the table above: `keywords`, `max_items`, `sort_by`, `note_type`, `time_filter`, `timeout_secs`.
