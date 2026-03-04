# Node: supabase.execute

**Category**: connector.data
**Description**: Execute CRUD operations on Supabase database tables

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `supabase` | Credential name in vault |
| `operation` | `string` | Yes | `-` | Operation type: 'select', 'insert', 'update', 'delete', or 'upsert' |
| `table` | `string` | Yes | `-` | Table name |
| `schema` | `string` | No | `public` | Database schema (default: 'public') |
| `data` | `any` | No | `None` | Data for insert/update/upsert operations (dict or list of dicts) |
| `filters` | `any` | No | `None` | Filter conditions for select/update/delete (e.g., {'id': {'eq': '123'}}) |
| `columns` | `any` | No | `None` | Column names to return for select (default: all columns) |
| `limit` | `any` | No | `None` | Limit results for select |
| `offset` | `any` | No | `None` | Offset for pagination in select |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `operation` | `string` | - |
| `table` | `string` | - |
| `data` | `any` | - |
| `count` | `any` | - |
