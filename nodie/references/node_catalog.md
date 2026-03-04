# Nodie Node Catalog

Quick index for selecting nodes. For exact parameter schemas, read `{baseDir}/references/nodes/<node_type>.md`.

## Triggers & Control Flow

| Node | Purpose | Auth |
|------|---------|------|
| trigger.manual | Manual trigger — entry point for all workflows | — |
| input | Pause workflow and wait for user input (multi-question forms) | — |
| if | Conditional routing based on expression | — |
| loop | Iterate over array with sub-workflow per item | — |
| code | Execute Python in sandbox (data transform, filtering, formatting) | — |
| output | Define workflow outputs (text, image, video, json, markdown, file) | — |

## Data & HTTP

| Node | Purpose | Auth |
|------|---------|------|
| http_request | Make HTTP requests (GET/POST/PUT/DELETE) to external APIs | optional credential |
| rss.read | Fetch and parse RSS/Atom feeds | — |
| storage.get | Retrieve data from S3, KV storage, or HTTP URL | — |
| storage.store | Store data to S3 or KV storage | — |
| markdown.convert | Convert between Markdown and HTML | — |

## Social Media & Search (zero-auth)

| Node | Purpose | Auth |
|------|---------|------|
| xhs.search | Search Xiaohongshu (RedNote) posts by keyword | zero-auth |
| xhs.get_comments | Scrape comment content from XHS posts | zero-auth |
| twitter.search | Search Twitter/X tweets by keyword or user | zero-auth (apify) |
| reddit.search | Search Reddit posts, subreddits, or users | zero-auth (apify) |
| youtube.search | Search YouTube videos, channels, or playlists | zero-auth (apify) |
| youtube.get_videos | Get detailed info about YouTube videos | zero-auth (apify) |
| youtube.get_channel | Get YouTube channel info | zero-auth (apify) |
| instagram.search | Search and scrape Instagram hashtags, users, or places | zero-auth (apify) |
| linkedin.search | Search LinkedIn job postings | zero-auth (apify) |
| discord.messages | Read messages from a Discord channel | — |
| video.fetch | Get direct video URL from Bilibili, YouTube, XHS, TikTok, etc. | zero-auth |

## Messaging

| Node | Purpose | Auth |
|------|---------|------|
| email.send | Send email via SMTP (TLS/SSL, HTML, CC/BCC) | smtp credential |
| gmail.send | Send email via Gmail | google credential |
| gmail.list | List/search emails from Gmail | google credential |
| gmail.get | Get email details from Gmail | google credential |
| slack.post_message | Post a message to a Slack channel | slack credential |
| slack.interactive_message | Send interactive buttons for approval workflows | slack credential |
| feishu.send_card | Send messages/cards to Feishu (飞书) | feishu credential |

## Productivity

| Node | Purpose | Auth |
|------|---------|------|
| notion.create_page | Create a page in a Notion database | notion credential |
| notion.get_page | Get a Notion page by ID | notion credential |
| notion.get_database | Get Notion database schema | notion credential |
| notion.query_database | Query entries from a Notion database | notion credential |
| notion.update_page | Update a Notion page's properties | notion credential |
| notion.append_blocks | Append blocks to a Notion page (images, text, etc.) | notion credential |
| google_sheets.get | Get data from a Google Spreadsheet | google credential |
| google_sheets.append_rows | Append rows to a Google Sheet | google credential |
| google_sheets.create | Create a new Google Spreadsheet | google credential |
| google_docs.create | Create a new Google Doc | google credential |
| google_docs.get | Get content from a Google Doc | google credential |
| google_docs.update | Update a Google Doc | google credential |
| google_drive.list | List files/folders in Google Drive | google credential |
| google_drive.upload | Upload a file to Google Drive | google credential |
| google_drive.download | Download a file from Google Drive | google credential |
| google_drive.get | Get file metadata from Google Drive | google credential |
| google_drive.create_folder | Create a Google Drive folder | google credential |
| airtable.append_rows | Append rows to an Airtable table | airtable credential |
| feishu.bitable_append | Append record to Feishu Bitable (多维表格) | feishu credential |
| trello.create_card | Create a card in a Trello board | trello credential |
| supabase.execute | CRUD operations on Supabase tables | supabase credential |
| supabase.batch | Multiple parallel Supabase queries | supabase credential |

## Developer

| Node | Purpose | Auth |
|------|---------|------|
| github.get_issues | Get issues/PRs from a GitHub repository | github credential |

## AI

| Node | Purpose | Auth |
|------|---------|------|
| openai_chat | GPT-4/3.5 text generation (summarize, analyze, write) | $env['OPENAI_API_KEY'] |
| claude.chat | Claude text generation | $env['CLAUDE_API_KEY'] |
| gemini.chat | Gemini text generation | $env['GEMINI_API_KEY'] |
| openai.image | Image generation (DALL-E, Gemini) | $env['OPENAI_API_KEY'] |
| gemini.image_edit | Image editing (style transfer, filters) | $env['OPENAI_API_KEY'] |
| gemini.video | Video generation from text (Veo) | $env['OPENAI_API_KEY'] |
| gemini.video_analysis | Analyze video content with Gemini | $env['OPENAI_API_KEY'] |
| assemblyai.transcribe | Speech-to-text + speaker diarization (AssemblyAI) | — |
| xfyun.transcribe | Speech-to-text + speaker diarization (讯飞) | — |
