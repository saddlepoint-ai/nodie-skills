# Node: ffmpeg.extract_audio

**Category**: connector.media
**Description**: 视频提取音频 (FFmpeg)

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `video_url` | `string` | Yes | `-` | 视频文件 URL (S3/HTTP，需公开可访问) |
| `audio_format` | `string` | No | `mp3` | 输出音频格式: mp3, wav, aac, flac |
| `audio_quality` | `string` | No | `192k` | 音频比特率: 64k, 128k, 192k, 256k, 320k |

## Output

| Field | Type | Description |
|-------|------|-------------|
| `audio_url` | `string` | 提取后的音频 S3 URL |
| `duration` | `any` | 音频时长 (秒) |
| `file_size` | `integer` | 文件大小 (字节) |
| `original_video` | `string` | 原视频 URL |
