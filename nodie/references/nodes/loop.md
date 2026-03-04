# Node: loop

**Category**: core
**Description**: Iterate over array with external calls (LLM/API/email) per item. For simple list transforms, use code node instead.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `items` | `any` | Yes | `-` | Array to iterate over. Can be a reference like $node["items"] |
| `max_iterations` | `integer` | No | `1000` | Maximum number of iterations (safety limit) |
| `parallel` | `boolean` | No | `False` | Execute iterations in parallel for faster processing |
| `max_concurrency` | `integer` | No | `5` | Maximum concurrent executions when parallel=True |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `results` | `array` | Results from each iteration |
| `count` | `integer` | Number of iterations executed |
