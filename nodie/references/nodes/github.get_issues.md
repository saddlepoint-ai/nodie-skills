# Node: github.get_issues

**Category**: connector.developer
**Description**: Get issues and pull requests from a GitHub repository

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `github` | Credential name in vault |
| `owner` | `string` | Yes | `-` | Repository owner (user or organization) |
| `repo` | `string` | Yes | `-` | Repository name |
| `state` | `string` | No | `open` | Issue state: 'open', 'closed', or 'all' |
| `labels` | `any` | No | `None` | Filter by labels |
| `assignee` | `any` | No | `None` | Filter by assignee username |
| `creator` | `any` | No | `None` | Filter by creator username |
| `sort` | `string` | No | `created` | Sort by: 'created', 'updated', 'comments' |
| `direction` | `string` | No | `desc` | Sort direction: 'asc' or 'desc' |
| `per_page` | `integer` | No | `30` | Results per page (max 100) |
| `max_pages` | `integer` | No | `1` | Maximum pages to fetch |
| `include_pull_requests` | `boolean` | No | `True` | Include pull requests in results |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `issues` | `array` | - |
| `total_count` | `integer` | - |
| `has_more` | `boolean` | - |
