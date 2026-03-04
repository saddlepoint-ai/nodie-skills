# Node: assemblyai.transcribe

**Category**: connector.ai
**Description**: 语音转文字 + 说话人识别 (AssemblyAI)

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `audio_url` | `string` | Yes | `-` | 音频文件 URL (S3/HTTP，需公开可访问) |
| `language_code` | `any` | No | `None` | 语言代码 (zh/en/ja 等)，不设置则自动检测 |
| `speaker_labels` | `boolean` | No | `True` | 开启说话人识别 |
| `speakers_expected` | `any` | No | `None` | 预期说话人数量 (可选) |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `text` | `string` | 完整转录文本 |
| `utterances` | `array` | 按说话人分段 |
| `speakers` | `array` | 识别到的说话人列表 |
| `confidence` | `any` | 置信度 |
| `audio_duration` | `any` | 音频时长 (毫秒) |
