# Node: notion.append_blocks

**Category**: connector.productivity
**Description**: Append child blocks to a Notion page or block

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `notion` | Credential name in vault |
| `block_id` | `string` | Yes | `-` | ID of the Notion block (usually a page ID) to append children to |
| `blocks` | `array` | Yes | `-` | List of block objects to append (Notion API block format) |

## Block Format

Each block in the `blocks` array must follow Notion API block format:

### Image Block
```json
{
  "object": "block",
  "type": "image",
  "image": {
    "type": "external",
    "external": {
      "url": "https://example.com/image.png"
    }
  }
}
```

### Paragraph Block
```json
{
  "object": "block",
  "type": "paragraph",
  "paragraph": {
    "rich_text": [
      {
        "type": "text",
        "text": {
          "content": "Your text here"
        }
      }
    ]
  }
}
```

### Heading Block (H1)
```json
{
  "object": "block",
  "type": "heading_1",
  "heading_1": {
    "rich_text": [
      {
        "type": "text",
        "text": {
          "content": "Heading text"
        }
      }
    ]
  }
}
```

### Using Previous Node Output
To reference output from a previous node (e.g., image URL from `openai.image`):
```json
{
  "object": "block",
  "type": "image",
  "image": {
    "type": "external",
    "external": {
      "url": "$previous_node_id['results'][0]"
    }
  }
}
```

## Example

```json
{
  "credential": "notion",
  "block_id": "3030aabdb48180288709d97b37131bbe",
  "blocks": [
    {
      "object": "block",
      "type": "paragraph",
      "paragraph": {
        "rich_text": [
          {
            "type": "text",
            "text": {
              "content": "Generated avatar:"
            }
          }
        ]
      }
    },
    {
      "object": "block",
      "type": "image",
      "image": {
        "type": "external",
        "external": {
          "url": "$openai_image_1['results'][0]"
        }
      }
    }
  ]
}
```

## Output

| Field | Type | Description |
|-------|------|-------------|
| `results` | `array` | Array of created block objects (Notion API format) |
