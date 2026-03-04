# Node: gemini.video_analysis

**Category**: connector.ai
**Description**: Analyze video content using Gemini via OpenAI-compatible API

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `video_url` | `string` | Yes | `-` | URL of the video to analyze |
| `prompt` | `string` | Yes | `-` | Prompt for the analysis (e.g. 'Describe what happens in this video') |
| `api_key` | `any` | No | `None` | API key. Auto-loaded from OPENAI_API_KEY env if not provided. |
| `base_url` | `any` | No | `None` | API base URL. Auto-loaded from OPENAI_BASE_URL env if not provided. |
| `model` | `string` | No | `gemini-2.0-flash` | Model to use (gemini-2.0-flash, gemini-1.5-pro, etc.) |
| `max_tokens` | `any` | No | `None` | Maximum tokens to generate |
| `temperature` | `number` | No | `0.7` | Sampling temperature (0-2) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `content` | `string` | Analysis result text |
| `model` | `string` | Model used |
| `tokens` | `object` | Token usage details |
| `finish_reason` | `string` | Why generation stopped |
