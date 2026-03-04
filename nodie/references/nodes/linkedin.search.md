# Node: linkedin.search

**Category**: connector.data
**Description**: Search LinkedIn job postings

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `apify_system` | Credential: 'apify' (user or system fallback) or 'apify_system' (system-level only) |
| `job_titles` | `array` | Yes | `-` | Job titles to search for (e.g., ['Software Engineer', 'Backend Developer']) |
| `locations` | `any` | No | `None` | Locations to filter by (e.g., ['San Francisco, CA', 'New York, NY']) |
| `companies` | `any` | No | `None` | Company names to filter by (e.g., ['Google', 'Meta']) |
| `max_items` | `integer` | No | `25` | Maximum number of jobs to return (1-500) |
| `workplace_type` | `any` | No | `None` | Workplace type filter |
| `employment_type` | `any` | No | `None` | Employment type filter |
| `experience_level` | `any` | No | `None` | Experience level filter |
| `posted_within` | `any` | No | `None` | Filter jobs posted within time period |
| `timeout_secs` | `integer` | No | `300` | Timeout in seconds for the search operation |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `jobs` | `array` | List of job objects |
| `total` | `integer` | Number of jobs returned |
