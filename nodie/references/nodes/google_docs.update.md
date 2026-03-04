# Node: google_docs.update

**Category**: connector.productivity
**Description**: Update a Google Doc

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `google` | Credential: 'google' (OAuth) or 'google_service_account' (SA, for shareable link) |
| `document_id` | `any` | No | `None` | Document ID (alternative to document_url) |
| `document_url` | `any` | No | `None` | Shareable document URL (alternative to document_id) |
| `operation` | `string` | Yes | `-` | Operation: append_text or replace_text |
| `text` | `any` | No | `None` | Text to append |
| `find_text` | `any` | No | `None` | Text to find |
| `replace_text` | `any` | No | `None` | Replacement text |
| `match_case` | `boolean` | No | `False` | Match case for find/replace |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `document_id` | `string` | - |
| `success` | `boolean` | - |
| `operation` | `string` | - |
| `occurrences_replaced` | `any` | - |
