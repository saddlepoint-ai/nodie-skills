# Node: output

**Category**: end
**Description**: Define and display workflow outputs

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `outputs` | `array` | Yes | `-` | List of outputs to save/display. Each output has type, value, and optional label. |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `results` | `array` | List of output results |

## Examples

### Basic Usage (JSON)

```json
{
  "id": "output_1",
  "name": "完成",
  "type": "output",
  "params": {
    "outputs": [
      {
        "type": "markdown",
        "label": "生成完成",
        "value": "✨ **创意头像已生成并保存到 Notion**\n\n🎨 **头像1**: 赛博朋克风格\n- 采用霓虹色和几何图案\n- 高清质量 (1024x1024)\n\n🎨 **头像2**: 水彩艺术风格\n- 采用柔和颜色和艺术笔触\n- 高清质量 (1024x1024)\n\n✅ 已保存到 Notion 页面"
      }
    ]
  },
  "position": {
    "x": 1392,
    "y": 0
  }
}
```

### Markdown Table Pattern (JSON)

For complex formatting like Markdown tables, use a `code` node to prepare the formatted string first:

```json
{
  "id": "format_results",
  "type": "code",
  "name": "Format Results",
  "params": {
    "posts": "$search_reddit['posts']",
    "code": "posts = input.get('posts', [])\ntable_rows = []\nfor i, post in enumerate(posts, 1):\n    short_title = (post['title'][:30] + '...') if len(post['title']) > 30 else post['title']\n    row = f\"| {i} | {short_title} | {post['author']} |\"\n    table_rows.append(row)\nresult = {'table_text': '\\n'.join(table_rows)}"
  },
  "next": ["output_1"]
},
{
  "id": "output_1",
  "name": "Complete",
  "type": "output",
  "params": {
    "outputs": [
      {
        "type": "markdown",
        "label": "Reddit Posts",
        "value": "📊 **Reddit OpenClaw Search Results**\n\n| # | Title | Author |\n|---|-------|--------|\n${{ format_results['table_text'] }}"
      }
    ]
  },
  "position": {
    "x": 992,
    "y": 0
  }
}
```

## Important Notes

**CRITICAL: Markdown formatting in `value` field:**
- The `${{ }}` syntax in the `value` field ONLY supports simple path references (e.g., `${{ node_id['field'] }}`)
- DO NOT use JavaScript/Python expressions like `.map()`, `.join()`, `.substring()`, or any logic inside `${{ }}`
- For complex Markdown formatting (tables, lists from arrays), ALWAYS use a `code` node before the `output` node to prepare the formatted string, then reference it in the output node (e.g., `${{ code_node['table_text'] }}`)
