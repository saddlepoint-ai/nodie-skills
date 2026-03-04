# Node: apify.get_dataset

**Category**: connector.scraping
**Description**: Get items from an Apify Dataset

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `apify` | Credential: 'apify' (user or system fallback) or 'apify_system' (system-level only) |
| `dataset_id` | `string` | Yes | `-` | Dataset ID to retrieve items from |
| `offset` | `integer` | No | `0` | Number of items to skip |
| `limit` | `integer` | No | `1000` | Maximum number of items to return |
| `fields` | `any` | No | `None` | Only return these fields from each item |
| `clean` | `boolean` | No | `True` | Remove empty items and hidden fields |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `dataset_id` | `string` | Dataset ID |
| `items` | `array` | Dataset items |
| `count` | `integer` | Number of items returned |
| `total` | `any` | Total items in dataset |
| `has_more` | `boolean` | Whether more items exist |
