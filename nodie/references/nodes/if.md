# Node: if

**Category**: core
**Description**: Conditional routing based on expression evaluation

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `condition` | `string` | Yes | `-` | Python expression to evaluate. Use $node["field"] for references. Example: '$review["approved"] == true' |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `result` | `boolean` | Result of condition evaluation (true/false) |
| `condition` | `any` | The condition that was evaluated |
