# Node: openai.image

**Category**: connector.ai
**Description**: Generate images using OpenAI-compatible API (DALL-E, Gemini, etc.). Supports multiple models, sizes, and HD quality. Use for creating visual content, mockups, and illustrations.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `prompt` | `string` | Yes | `-` | Image generation prompt |
| `api_key` | `string` | Yes | `-` | OpenAI API key. Use ${{ env['OPENAI_API_KEY'] }} |
| `base_url` | `any` | No | `None` | Custom API base URL. Use ${{ env['OPENAI_BASE_URL'] }} if needed |
| `size` | `string` | No | `1024x1024` | Image size: 1024x1024, 1024x1792, 1792x1024 |
| `quality` | `string` | No | `standard` | Image quality: standard or hd |
| `n` | `integer` | No | `1` | Number of images to generate (1-10) |
| `model` | `string` | No | `dall-e-3` | Model to use: dall-e-2, dall-e-3, gemini-2.5-flash-image-preview, etc. |
| `response_format` | `string` | No | `auto` | Response format: 'url', 'b64_json', or 'auto' (auto-detect from response) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `url` | `string` | - |
| `revised_prompt` | `any` | - |
