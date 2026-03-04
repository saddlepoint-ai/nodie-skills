# Node: markdown.convert

**Category**: connector.data
**Description**: Convert between Markdown and HTML. Use markdownToHtml for email bodies and web content, htmlToMarkdown for content extraction.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `mode` | `string` | Yes | `-` | Conversion mode: 'markdownToHtml' or 'htmlToMarkdown' |
| `content` | `string` | Yes | `-` | Content to convert |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `converted` | `string` | - |
