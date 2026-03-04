# Node: gemini.video

**Category**: connector.ai
**Description**: Generate videos from text using Gemini Veo

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `prompt` | `string` | Yes | `-` | Description of the video to generate |
| `api_key` | `string` | Yes | `-` | API key. Use $env['OPENAI_API_KEY'] |
| `base_url` | `string` | No | `https://api.nuwaapi.com/v1` | API base URL. Use $env['OPENAI_BASE_URL'] |
| `model` | `string` | No | `veo3.1-components` | Model to use for video generation (e.g., veo3.1-components, veo3.1). Official Vertex ID: veo-3.1-generate-preview |
| `aspect_ratio` | `string` | No | `16:9` | Aspect ratio for the generated video (e.g., '16:9', '9:16') |
| `duration_seconds` | `integer` | No | `5` | Length of the generated video in seconds (typically 5 or 8) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `url` | `string` | URL of the generated video (S3) |
