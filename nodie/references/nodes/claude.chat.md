# Node: claude.chat

**Category**: connector.ai
**Description**: Generate text using Claude Chat API. Use for summarization, content generation, analysis, and AI-powered text processing.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `prompt` | `string` | Yes | `-` | User prompt/message |
| `api_key` | `string` | Yes | `-` | Claude API key. Use ${{ env['CLAUDE_API_KEY'] }} |
| `system_prompt` | `any` | No | `None` | System prompt (optional) |
| `model` | `string` | No | `claude-sonnet-4-5-20250929` | Model to use (claude-sonnet-4-5-20250929, claude-opus-4-5-20251101, etc.) |
| `temperature` | `number` | No | `0.7` | Sampling temperature (0-2) |
| `max_tokens` | `any` | No | `None` | Maximum tokens to generate |
| `base_url` | `any` | No | `None` | Custom API base URL. Default: https://api.nuwaapi.com/v1 |
| `response_format` | `string` | No | `text` | Response format: 'text' or 'json_object' |
| `image_url` | `any` | No | `None` | Image URL for Vision analysis (supports http/https URLs) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `content` | `string` | AI response text |
| `model` | `string` | Model used (e.g., claude-sonnet-4-5-20250929) |
| `tokens` | `integer` | Total tokens used |
| `finish_reason` | `string` | Why generation stopped |
