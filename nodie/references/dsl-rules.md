# Nodie DSL Rules

## Core Concepts

A workflow is a **list of nodes** connected into a pipeline by the `next` field.

```
trigger → node_a → node_b → output
```

Each node has:
- **`id`** — unique identifier (snake_case, e.g. `fetch_news_1`)
- **`type`** — registered node type (e.g. `xhs.search`, see node_catalog.md)
- **`name`** — display name (Title Case)
- **`params`** — node-specific configuration (see per-node docs in `references/nodes/`)
- **`next`** — array of node IDs this node connects to (controls execution order)

### How `next` works

`next` defines the execution DAG — which nodes run after the current one finishes.

```yaml
next: [step_2]                    # Sequential: run step_2 after this
next: [branch_a_1, branch_b_1]   # Parallel: run both branches
next: []                          # Terminal: workflow ends here
# Omitting next entirely also means terminal
```

**Every non-terminal node MUST have `next`.** Nodes without `next` are dead ends — their output is unreachable.

### How `params` and context references work

`params` contains the configuration values for a node. Within params, you can reference outputs from earlier nodes:

```yaml
# Direct reference — use the full output or a specific field
params:
  data: $fetch_data_1                   # entire output of fetch_data_1
  body: $fetch_data_1['body']           # specific field
  api_key: $env['OPENAI_API_KEY']       # environment variable

# String interpolation — embed references inside text
params:
  prompt: "Summarize: ${{ articles_1['content'] }}"
```

**`${{ }}` supports ONLY simple path references** like `${{ node_id['field'] }}`. No JavaScript/Python expressions (`.map()`, `.join()`, etc.) — use a `code` node for complex formatting, then reference its output.

## Minimal Example

```yaml
name: Search XHS
nodes:
  - id: trigger_1
    type: trigger.manual
    name: Start
    params: {}
    next: [search_1]

  - id: search_1
    type: xhs.search
    name: Search XHS
    params:
      keywords: "coffee"
      max_items: 10
    next: [output_1]

  - id: output_1
    type: output
    name: Results
    params:
      outputs:
        - type: json
          value: $search_1
          label: "Search Results"
    next: []
```

## Schema Reference (strict — extra fields are REJECTED)

The engine validates DSL with Pydantic `extra="forbid"`. Any field not listed below causes a parse error.

### Workflow Top-Level

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string (1-100 chars) | ✓ | Workflow display name |
| `nodes` | array of Node | ✓ | At least 1 node |
| `id` | string | optional | Auto-generated if omitted |
| `description` | string | optional | Workflow description |

### Node Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | string | ✓ | Unique, snake_case (e.g. `fetch_news_1`) |
| `type` | string | ✓ | Registered node type (see node_catalog.md) |
| `name` | string (1-100 chars) | ✓ | Display name, Title Case |
| `params` | object | optional | Node parameters (default `{}`) |
| `next` | array of string | optional | Next node IDs for execution flow |
| `body` | object | optional | Only for `loop` nodes (sub-workflow) |
| `disabled` | boolean | optional | Skip this node (default false) |
| `position` | `{x, y}` | optional | UI canvas position |

**Forbidden fields**: `label`, `config`, `action`, `description`, `edges`, `connections`, `inputs`, `outputs`, or anything not listed above.

## Validation Rules

1. **Entry node must be trigger**: The first node MUST have `type` starting with `trigger.`.
2. **Unique IDs**: All node `id` values must be unique.
3. **Valid `next` references**: Every ID in `next` must match an existing node `id`.
4. **Valid param references**: `$node_id` — `node_id` must be an existing node in the workflow.

## Special Node Patterns

### Code Nodes

```yaml
- id: transform_1
  type: code
  name: Transform Data
  params:
    input_data: $previous_1['output']
    code: |
      data = input['input_data']
      result = {'processed': len(data)}
```

Access inputs via `input['param_name']`. Set output via `result = {...}`.

### Loop Nodes

`body` is at the **top level** of the node (NOT inside `params`):

```yaml
- id: process_items_1
  type: loop
  params:
    items: $upstream_1['items']
  body:
    entry: [sub_step_1]
    nodes:
      - id: sub_step_1
        type: code
        name: Process Item
        params:
          data: $item
        next: []
  next: [after_loop_1]
```

### Output Nodes

```yaml
- id: output_1
  type: output
  name: Output
  params:
    outputs:
      - type: text
        value: $summarize_1['content']
        label: "Summary"
      - type: image
        value: $image_gen_1['results']
        label: "Images"
  next: []
```

Output `type` can be: `text`, `image`, `video`, `json`, `markdown`, `file`.
