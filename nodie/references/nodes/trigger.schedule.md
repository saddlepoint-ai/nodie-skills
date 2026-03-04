# Node: trigger.schedule

**Category**: starter
**Description**: Trigger workflow on a schedule using cron expressions or intervals. Use for daily/weekly/hourly automated tasks.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `mode` | `string` | No | `interval` | Schedule mode: 'cron' or 'interval' |
| `cron` | `any` | No | `None` | Cron expression (e.g., '0 9 * * *' for 9am daily) |
| `interval_value` | `any` | No | `None` | Interval value (e.g., 1, 5, 15) |
| `interval_unit` | `any` | No | `None` | Interval unit: 'minutes', 'hours', 'days', 'weeks' |
| `timezone` | `string` | No | `UTC` | Timezone for schedule |
| `paused` | `boolean` | No | `False` | Whether the schedule is paused |
| `start_time` | `any` | No | `None` | Start time (ISO format) |
| `end_time` | `any` | No | `None` | End time (ISO format) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `mode` | `string` | - |
| `schedule_config` | `object` | - |
| `triggered_at` | `string` | - |
| `next_trigger` | `any` | - |
