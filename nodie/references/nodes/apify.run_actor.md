# Node: apify.run_actor

**Category**: connector.scraping
**Description**: Run an Apify Actor and get results

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `credential` | `string` | No | `apify` | Credential: 'apify' (user or system fallback) or 'apify_system' (system-level only) |
| `actor_id` | `string` | Yes | `-` | Actor ID (e.g., 'apify/web-scraper' or 'username/actor-name') |
| `input` | `any` | No | `None` | Input object for the Actor (actor-specific configuration) |
| `build` | `any` | No | `None` | Build tag or number to run (default: latest) |
| `timeout_secs` | `integer` | No | `300` | Timeout in seconds for Actor run (max wait time) |
| `memory_mbytes` | `any` | No | `None` | Memory limit in MB (128, 256, 512, 1024, 2048, 4096) |
| `wait_for_finish` | `boolean` | No | `True` | Wait for Actor to finish and return results |
| `poll_interval_secs` | `integer` | No | `5` | Polling interval in seconds when waiting for finish |
| `upload_to_s3` | `boolean` | No | `False` | Auto-download media files (images/videos) and upload to S3, replacing temporary URLs with permanent S3 URLs |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `run_id` | `string` | Unique ID of the Actor run |
| `actor_id` | `string` | Actor ID that was run |
| `status` | `string` | Run status (SUCCEEDED, FAILED, RUNNING, etc.) |
| `started_at` | `string` | When the run started |
| `finished_at` | `any` | When the run finished |
| `default_dataset_id` | `string` | ID of the default dataset |
| `default_key_value_store_id` | `string` | ID of the default key-value store |
| `stats` | `any` | Run statistics |
| `items` | `any` | Dataset items if wait_for_finish=True |
| `items_count` | `integer` | Number of items in dataset |
