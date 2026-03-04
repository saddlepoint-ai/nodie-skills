# Node: openai.image_edit

**Category**: ai.image
**Description**: Edit images using DALL-E 2 (replace backgrounds, modify scenes)

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `image_url` | `string` | Yes | `-` | URL of the image to edit. Will be downloaded and converted to PNG. |
| `prompt` | `string` | Yes | `-` | Description of the edit to make (e.g., 'Replace background with office scene') |
| `api_key` | `string` | Yes | `-` | OpenAI API key. Use ${{ env['OPENAI_API_KEY'] }} |
| `base_url` | `any` | No | `None` | Custom API base URL. Use ${{ env['OPENAI_BASE_URL'] }} if needed |
| `model` | `string` | No | `dall-e-2` | Model to use for image editing. Only dall-e-2 supports editing. |
| `size` | `string` | No | `1024x1024` | Output image size: 256x256, 512x512, or 1024x1024 |
| `num` | `integer` | No | `1` | Number of images to generate (1-10) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `url` | `string` | URL of the edited image |
| `original_url` | `string` | URL of the original image |
