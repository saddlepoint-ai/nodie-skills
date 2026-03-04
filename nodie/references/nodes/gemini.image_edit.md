# Node: gemini.image_edit

**Category**: connector.ai
**Description**: Edit images using Gemini (style transfer, filters, artistic effects)

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `image_url` | `any` | Yes | `-` | URL(s) of the image(s) to edit. Can be a single URL string or a list of URL strings. |
| `prompt` | `string` | Yes | `-` | Description of the edit (e.g., 'Convert to elegant greyscale with vintage film look') |
| `api_key` | `string` | Yes | `-` | API key. Use $env['OPENAI_API_KEY'] |
| `base_url` | `string` | No | `https://api.nuwaapi.com/v1` | API base URL. Use $env['OPENAI_BASE_URL'] |
| `model` | `string` | No | `gemini-2.5-flash-image-preview` | Model to use for image editing |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `urls` | `array` | URLs of the edited images (S3) |
| `original_urls` | `any` | URLs of the original images |
