# Node: xfyun.transcribe

**Category**: connector.ai
**Description**: 语音转文字 + 说话人识别 (讯飞开放平台)

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `audio_url` | `string` | Yes | `-` | 音频文件 URL (需公开可访问) |
| `language` | `string` | No | `cn` | 语言: cn(中文), en(英文), ja(日语), ko(韩语)... |
| `role_type` | `integer` | No | `1` | 角色分离: 0=关闭, 1=开启 |
| `role_num` | `any` | No | `None` | 说话人数量 (0=自动识别, 1-10=指定数量) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `text` | `string` | 完整转录文本 |
| `utterances` | `array` | 按说话人分段 |
| `speakers` | `array` | 识别到的说话人列表 |
| `duration` | `any` | 音频时长 (毫秒) |
| `order_id` | `any` | 讯飞订单 ID |
