# Node: supabase.batch

**Category**: connector.data
**Description**: Execute multiple Supabase queries in parallel using a single connection

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `supabase` | Credential name in vault |
| `queries` | `array` | Yes | `-` | List of queries to execute in parallel |
| `fail_fast` | `boolean` | No | `False` | If true, stop all queries if any query fails |

## Output

Output from supabase.batch node.
