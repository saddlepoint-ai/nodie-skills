# Node: openai_chat

**Category**: connector.ai
**Description**: Generate text using OpenAI Chat API (GPT-4, GPT-3.5). Use for summarization, content generation, analysis, and AI-powered text processing.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `prompt` | `string` | Yes | `-` | User prompt/message |
| `api_key` | `string` | Yes | `-` | OpenAI API key. Use ${{ env['OPENAI_API_KEY'] }} |
| `system_prompt` | `any` | No | `None` | System prompt (optional) |
| `model` | `string` | No | `gpt-4o-mini` | Model to use (gpt-4o-mini, gpt-4o, etc.) |
| `temperature` | `number` | No | `0.7` | Sampling temperature (0-2) |
| `max_tokens` | `any` | No | `None` | Maximum tokens to generate |
| `base_url` | `any` | No | `None` | Custom API base URL. Use ${{ env['OPENAI_BASE_URL'] }} if needed |
| `response_format` | `string` | No | `text` | Response format: 'text' or 'json_object' |
| `image_url` | `any` | No | `None` | Image URL for Vision analysis (supports http/https URLs) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `content` | `string` | AI response text |
| `model` | `string` | Model used (e.g., gpt-4) |
| `tokens` | `integer` | Total tokens used |
| `finish_reason` | `string` | Why generation stopped |
