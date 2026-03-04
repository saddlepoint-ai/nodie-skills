# Node: code

**Category**: core
**Description**: Execute Python code in a secure sandbox. Use for data transformation, filtering, formatting, and custom logic. Access inputs via input['param_name'], return via result = {...}. **IMPORTANT**: When generating Markdown tables or other formatted strings for output nodes, perform all formatting logic here (loops, string manipulation, etc.) and output a ready-to-use string field that can be directly referenced in the output node's `${{ }}` syntax.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `code` | `string` | Yes | `-` | Python code to execute. Access inputs via input['param_name'], return via result = {...} |

## Output

Code node output (flexible structure).

Allows any fields - actual structure depends on user code.
Actual output schema is determined by execution and cached by WorkflowManager.

## Important Notes

**CRITICAL: Formatting for Output Nodes**

When preparing data for `output` nodes (especially Markdown tables), all formatting logic must be done in the `code` node:

- ✅ **DO**: Generate formatted strings (e.g., `table_text`) in the code node, then reference `${{ code_node.table_text }}` in the output node
- ❌ **DON'T**: Try to use `.map()`, `.join()`, or other expressions inside `${{ }}` in output nodes

**Example - Generating Markdown Table:**
```yaml
- id: format_results
  type: code
  params:
    posts: $search_reddit['posts']
    code: |
      table_rows = []
      for i, post in enumerate(input['posts'], 1):
        short_title = (post['title'][:30] + '...') if len(post['title']) > 30 else post['title']
        row = f"| {i} | {short_title} | {post['author']} |"
        table_rows.append(row)
      result = {'table_text': '\n'.join(table_rows)}
  next: [output_1]

- id: output_1
  type: output
  params:
    outputs:
      - type: markdown
        value: |
          | # | Title | Author |
          |---|-------|--------|
          ${{ format_results.table_text }}
```

**Security:**
- Runs in RestrictedPython sandbox with blocklist-based security
- Most packages allowed including: praw, requests, httpx, beautifulsoup4, pandas, numpy, etc.
- BLOCKED modules: os, sys, subprocess, shutil, pathlib (system), socket, ssl (raw network), pickle, marshal (serialization), importlib, ctypes, gc (dangerous internals)
- NOT allowed: file I/O, eval, exec, open
