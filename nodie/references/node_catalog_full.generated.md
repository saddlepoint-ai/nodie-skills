# Nodie Node Reference

## Quick Index

- trigger.manual: Manual trigger that starts workflow with configured parameters. Use as entry point for on-demand workflows. [keywords: start, begin, manual, trigger, entry, webhook]
- trigger.schedule: Trigger workflow on a schedule using cron expressions or intervals. Use for daily/weekly/hourly automated tasks. [keywords: schedule, cron, timer, daily, weekly, hourly, interval, automated, recurring]
- input: Pause workflow and wait for user input (supports multiple questions) [keywords: input, user, form, upload, review, approval, human, questions]
- code: Execute Python code in a secure sandbox. Use for data transformation, filtering, formatting, and custom logic. Access inputs via input['param_name'], return via result = {...}. IMPORTANT: When generating Markdown tables or other formatted strings for output nodes, perform all formatting logic here (loops, string manipulation, etc.) and output a ready-to-use string field that can be directly referenced in the output node's ${{ }} syntax. [keywords: code, python, transform, filter, process, logic, script, compute, calculate, format, parse, markdown, table]
- http_request: Make HTTP requests to external APIs. Supports GET/POST/PUT/DELETE with headers, body, and query params. Use for fetching data from REST APIs. [keywords: http, api, rest, fetch, request, get, post, webhook, external, integration]
- if: Conditional routing based on expression evaluation [keywords: if, condition, branch, route, decision]
- loop: Iterate over array with external calls (LLM/API/email) per item. For simple list transforms, use code node instead. [keywords: loop, iterate, for, each, array, batch, repeat]
- storage.get: Retrieve data from S3, KV storage, or HTTP URL [keywords: storage, get, download, retrieve, file, s3, kv]
- storage.store: Store data to S3 or KV storage with URI-based backend selection [keywords: storage, save, upload, file, s3, kv, persist]
- output: Define and display workflow outputs [keywords: output, result, save, display, export]
- discord.messages: Read messages from a Discord channel [keywords: discord, messages, chat, community, gaming]
- instagram.search: Search and scrape Instagram hashtags, users, or places [keywords: instagram, search, hashtag, user, place, posts, scrape]
- linkedin.search: Search LinkedIn job postings [keywords: linkedin, jobs, search, career, hiring, recruitment, apify]
- markdown.convert: Convert between Markdown and HTML. Use markdownToHtml for email bodies and web content, htmlToMarkdown for content extraction. [keywords: markdown, html, convert, format, email, render, content, document]
- reddit.search: Search Reddit posts, subreddits, or users [keywords: reddit, search, posts, social, forum, apify]
- rss.read: Fetch and parse RSS/Atom feeds. Returns list of articles with title, link, description, content, published date, and author. Use for news aggregation and content monitoring. [keywords: rss, feed, atom, news, articles, blog, subscribe, content, aggregation, monitor]
- supabase.batch: Execute multiple Supabase queries in parallel using a single connection [keywords: supabase, database, batch, parallel, postgres, sql]
- supabase.execute: Execute CRUD operations on Supabase database tables [keywords: supabase, database, crud, postgres, sql]
- twitter.search: Search Twitter (X) tweets by keyword or user [keywords: twitter, x, tweets, search, social, apify]
- video.fetch: Fetch direct video URL from various platforms (Xiaohongshu, Bilibili, YouTube, etc.) [keywords: video, download, fetch, url, extract, xiaohongshu, 小红书, rednote, bilibili, b站, youtube, tiktok, 抖音, instagram, reels]
- xhs.get_comments: Scrape actual comment content from Xiaohongshu posts via comment_v2_sync. Uses system env XHS_APP_API_KEY. REQUIRED for sentiment/reputation analysis. Use after xhs.search to get comments from high-engagement notes. Returns full comment text, user info, likes, and nested replies. [keywords: xiaohongshu, 小红书, rednote, xhs, comments, scrape, social, china, comment_v2_sync]
- xhs.search: Search Xiaohongshu (RedNote) notes by keyword via search_v2_sync. Uses system env XHS_APP_API_KEY. Returns note metadata and engagement COUNTS only, NOT actual comment content. For sentiment/comment analysis, use xhs.get_comments. [keywords: xiaohongshu, 小红书, rednote, xhs, search, notes, social, china, app_search]
- youtube.get_channel: Get information about a YouTube channel using Apify [keywords: youtube, channel, subscribers, creator, apify]
- youtube.get_videos: Get detailed information about YouTube videos using Apify [keywords: youtube, video, statistics, details, views, likes, apify]
- youtube.search: Search YouTube for videos, channels, or playlists using Apify [keywords: youtube, search, video, channel, playlist, media, apify]
- email.send: Send emails via SMTP. Supports TLS/SSL, authentication, HTML content, and CC/BCC. Use for notifications, newsletters, and alerts. [keywords: email, smtp, send, mail, notify, newsletter, alert, message, communication]
- feishu.bitable_append: Append a record to a Feishu Bitable (飞书多维表格) [keywords: feishu, lark, 飞书, bitable, 多维表格, database, table, append]
- feishu.send_card: Send messages or interactive cards to Feishu (飞书) [keywords: feishu, lark, 飞书, message, card, notification, alert]
- gmail.get: Get email details from Gmail [keywords: google, gmail, email, get, read]
- gmail.list: List emails from Gmail [keywords: google, gmail, email, list, search]
- gmail.send: Send an email via Gmail [keywords: google, gmail, email, send, message]
- slack.interactive_message: Send an interactive message with buttons for approval workflows [keywords: slack, approval, interactive, button, approve, reject, workflow]
- slack.post_message: Post a message to a Slack channel [keywords: slack, message, notify, alert, chat]
- airtable.append_rows: Append rows to an Airtable table [keywords: airtable, database, append, record, data]
- google_docs.create: Create a new Google Doc [keywords: google, docs, create, document]
- google_docs.get: Get content from a Google Doc [keywords: google, docs, get, read, content]
- google_docs.update: Update a Google Doc [keywords: google, docs, update, append, replace]
- google_drive.create_folder: Create a folder in Google Drive [keywords: google, drive, folder, create, directory]
- google_drive.download: Download a file from Google Drive [keywords: google, drive, download, file]
- google_drive.get: Get file metadata from Google Drive [keywords: google, drive, get, metadata, file]
- google_drive.list: List files and folders in Google Drive [keywords: google, drive, list, files, folders]
- google_drive.upload: Upload a file to Google Drive [keywords: google, drive, upload, file]
- google_sheets.append_rows: Append rows to a Google Sheet [keywords: google sheets, spreadsheet, append, data, csv]
- google_sheets.create: Create a new Google Spreadsheet [keywords: google sheets, spreadsheet, create, new]
- google_sheets.get: Get data from a Google Spreadsheet [keywords: google sheets, spreadsheet, get, read, data]
- notion.append_blocks: Append child blocks to a Notion page or block [keywords: notion, page, block, append, content, image]
- notion.create_page: Create a page in a Notion database [keywords: notion, page, database, note, document]
- notion.get_database: Get a Notion database schema and metadata [keywords: notion, database, schema, get, retrieve]
- notion.get_page: Get a Notion page by ID [keywords: notion, page, get, read, retrieve]
- notion.query_database: Query entries from a Notion database [keywords: notion, database, query, search, filter]
- notion.update_page: Update a Notion page's properties [keywords: notion, page, update, edit, modify]
- trello.create_card: Create a card in a Trello board [keywords: trello, card, task, project, kanban]
- github.get_issues: Get issues and pull requests from a GitHub repository [keywords: github, issues, pull requests, pr, repository, git]
- assemblyai.transcribe: 语音转文字 + 说话人识别 (AssemblyAI) [keywords: speech, transcribe, audio, voice, speaker, diarization, 会议, 语音]
- claude.chat: Generate text using Claude Chat API. Use for summarization, content generation, analysis, and AI-powered text processing. [keywords: claude, anthropic, chat, ai, llm, generate, summarize, write, content, text, analysis]
- gemini.chat: Generate text using Gemini Chat API. Use for summarization, content generation, analysis, and AI-powered text processing. [keywords: gemini, google, chat, ai, llm, generate, summarize, write, content, text, analysis]
- gemini.image_edit: Edit images using Gemini (style transfer, filters, artistic effects) [keywords: gemini, image, edit, style, greyscale, filter, artistic]
- gemini.video: Generate videos from text using Gemini Veo [keywords: gemini, video, veo, generate, ai, content]
- gemini.video_analysis: Analyze video content using Gemini via OpenAI-compatible API [keywords: gemini, video, analysis, ai, content, google, visual]
- openai.image: Generate images using OpenAI-compatible API (DALL-E, Gemini, etc.). Supports multiple models, sizes, and HD quality. Use for creating visual content, mockups, and illustrations. [keywords: dalle, gemini, image, generate, ai, picture, visual, art, mockup, illustration, creative]
- openai_chat: Generate text using OpenAI Chat API (GPT-4, GPT-3.5). Use for summarization, content generation, analysis, and AI-powered text processing. [keywords: openai, gpt, chat, ai, llm, generate, summarize, write, content, text, analysis]
- xfyun.transcribe: 语音转文字 + 说话人识别 (讯飞开放平台) [keywords: speech, transcribe, audio, voice, speaker, diarization, 会议, 语音, 讯飞, xfyun]

---

## Nodes by Category

### Starter
*Workflow entry points - manual trigger, schedule, webhook*

#### trigger.manual [starter]
Manual trigger that starts workflow with configured parameters. Use as entry point for on-demand workflows.
Required: (none)

#### trigger.schedule [starter]
Trigger workflow on a schedule using cron expressions or intervals. Use for daily/weekly/hourly automated tasks.
Required: (none)
Optional: mode (string, default:'interval'), cron (any), interval_value (any), interval_unit (any), timezone (string, default:'UTC'), paused (boolean, default:False), start_time (any), end_time (any)
Output: mode (string), schedule_config (object), triggered_at (string), next_trigger (any)

### Input
*User interaction - pauses workflow for file upload, text input, approval*

#### input [input]
Pause workflow and wait for user input (supports multiple questions)
Required: questions (array)

### Core
*Core building blocks - code, loops, conditions, HTTP requests, storage*

#### code [core]
Execute Python code in a secure sandbox. Use for data transformation, filtering, formatting, and custom logic. Access inputs via input['param_name'], return via result = {...}. IMPORTANT: When generating Markdown tables or other formatted strings for output nodes, perform all formatting logic here (loops, string manipulation, etc.) and output a ready-to-use string field that can be directly referenced in the output node's ${{ }} syntax.
Required: code (string)

#### http_request [core]
Make HTTP requests to external APIs. Supports GET/POST/PUT/DELETE with headers, body, and query params. Use for fetching data from REST APIs.
Required: (none)
Optional: credential (any), body (any), params (any)
Output: status_code (integer), headers (object), body (any), elapsed_ms (number)

#### if [core]
Conditional routing based on expression evaluation
Required: condition (string)
Output: result (boolean), condition (any)

#### loop [core]
Iterate over array with external calls (LLM/API/email) per item. For simple list transforms, use code node instead.
Required: items (any)
Optional: max_iterations (integer, default:1000), parallel (boolean, default:False), max_concurrency (integer, default:5)
Output: results (array), count (integer)

#### storage.get [core]
Retrieve data from S3, KV storage, or HTTP URL
Required: key (string)
Optional: as_binary (boolean, default:False)
Output: content (any), binary_ref (any), backend (string), size (integer), content_type (any)

#### storage.store [core]
Store data to S3 or KV storage with URI-based backend selection
Required: content (any), key (string)
Optional: content_type (any), ttl (any)
Output: url (any), key (string), backend (string), size (integer)

### End
*Output placeholders - display text, image, video, audio, files*

#### output [end]
Define and display workflow outputs
Required: outputs (array)
Output: results (array)

### Connector - Social & Data
*Data sources from Social Media (YouTube, XHS, Twitter, Reddit, LinkedIn) and Databases.*

#### discord.messages [connector.data]
Read messages from a Discord channel
Required: channel_id (string)
Optional: limit (integer, default:100), keyword (any)
Output: messages (array), total (integer)

#### instagram.search [connector.data]
Search and scrape Instagram hashtags, users, or places
Required: (none)
Optional: credential (string, default:'apify_system'), search_type (string, default:'hashtag'), query (any), results_type (string, default:'posts'), search_limit (integer, default:5), results_limit (integer, default:20), direct_urls (any)
Output: items (array), total (integer), search_type (any), query (any)

#### linkedin.search [connector.data]
Search LinkedIn job postings
Required: job_titles (array)
Optional: credential (string, default:'apify_system'), locations (any), companies (any), max_items (integer, default:25), workplace_type (any), employment_type (any), experience_level (any), posted_within (any), ... (+1 more)
Output: jobs (array), total (integer)

#### markdown.convert [connector.data]
Convert between Markdown and HTML. Use markdownToHtml for email bodies and web content, htmlToMarkdown for content extraction.
Required: mode (string), content (string)
Output: converted (string)

#### reddit.search [connector.data]
Search Reddit posts, subreddits, or users
Required: query (string)
Optional: credential (string, default:'apify_system'), search_type (string, default:'search'), max_items (integer, default:25), sort (string, default:'relevance'), time_filter (string, default:'all'), include_comments (boolean, default:False), timeout_secs (integer, default:300)
Output: posts (array), total (integer)

#### rss.read [connector.data]
Fetch and parse RSS/Atom feeds. Returns list of articles with title, link, description, content, published date, and author. Use for news aggregation and content monitoring.
Required: url (string)
Optional: max_items (any)
Output: title (string), link (string), description (any), content (any), published (any), author (any)

#### supabase.batch [connector.data]
Execute multiple Supabase queries in parallel using a single connection
Required: queries (array)
Optional: credential (string, default:'supabase'), fail_fast (boolean, default:False)

#### supabase.execute [connector.data]
Execute CRUD operations on Supabase database tables
Required: operation (string), table (string)
Optional: credential (string, default:'supabase'), schema (string, default:'public'), data (any), filters (any), columns (any), limit (any), offset (any)
Output: operation (string), table (string), data (any), count (any)

#### twitter.search [connector.data]
Search Twitter (X) tweets by keyword or user
Required: query (string)
Optional: credential (string, default:'apify_system'), search_type (string, default:'keyword'), max_items (integer, default:25), sort_by (string, default:'Top'), lang (any, default:'en'), since_date (any), until_date (any), min_likes (any, default:5), ... (+9 more)
Output: tweets (array), total (integer)

#### video.fetch [connector.data]
Fetch direct video URL from various platforms (Xiaohongshu, Bilibili, YouTube, etc.)
Required: url (string)
Optional: timeout (integer, default:60), credential (string, default:'apify_system')
Output: video_url (string), platform (string), metadata (object)

#### xhs.get_comments [connector.data]
Scrape actual comment content from Xiaohongshu posts via comment_v2_sync. Uses system env XHS_APP_API_KEY. REQUIRED for sentiment/reputation analysis. Use after xhs.search to get comments from high-engagement notes. Returns full comment text, user info, likes, and nested replies.
Required: post_urls (array)
Optional: max_pages (any, default:3), sort_strategy (any, default:''), timeout_secs (integer, default:300)
Output: comments (array), total (integer)

#### xhs.search [connector.data]
Search Xiaohongshu (RedNote) notes by keyword via search_v2_sync. Uses system env XHS_APP_API_KEY. Returns note metadata and engagement COUNTS only, NOT actual comment content. For sentiment/comment analysis, use xhs.get_comments.
Required: keywords (any)
Optional: max_items (integer, default:20), sort_by (string, default:'general'), note_type (string, default:'all'), time_filter (any), timeout_secs (integer, default:300)
Output: notes (array), total (integer)

#### youtube.get_channel [connector.data]
Get information about a YouTube channel using Apify
Required: (none)
Optional: credential (string, default:'apify_system'), channel_id (any), for_handle (any), timeout_secs (integer, default:300)
Output: channel (any), found (boolean)

#### youtube.get_videos [connector.data]
Get detailed information about YouTube videos using Apify
Required: video_ids (any)
Optional: credential (string, default:'apify_system'), timeout_secs (integer, default:300)
Output: videos (array), count (integer)

#### youtube.search [connector.data]
Search YouTube for videos, channels, or playlists using Apify
Required: query (string)
Optional: credential (string, default:'apify_system'), max_results (integer, default:10), sort_order (any, default:'relevance'), date_filter (any), timeout_secs (integer, default:300)
Output: items (array), total_results (integer), video_ids (array)

### Connector - Messaging
*Messaging services - Slack, Email, Discord, Telegram*

#### email.send [connector.messaging]
Send emails via SMTP. Supports TLS/SSL, authentication, HTML content, and CC/BCC. Use for notifications, newsletters, and alerts.
Required: to (string), subject (string), body (string)
Optional: credential (any, default:'smtp'), content_type (string, default:'text/plain'), cc (any), bcc (any)
Output: success (boolean), message_id (any), recipients (array)

#### feishu.bitable_append [connector.messaging]
Append a record to a Feishu Bitable (飞书多维表格)
Required: app_token (string), table_id (string), fields (object)
Optional: credential (string, default:'feishu')
Output: record_id (string), status (string)

#### feishu.send_card [connector.messaging]
Send messages or interactive cards to Feishu (飞书)
Required: receive_id (string), content (any)
Optional: credential (string, default:'feishu'), receive_id_type (string, default:'open_id'), msg_type (string, default:'interactive')
Output: message_id (string), status (string)

#### gmail.get [connector.messaging]
Get email details from Gmail
Required: message_id (string)
Optional: credential (string, default:'google'), format (string, default:'full')
Output: message_id (string), thread_id (string), from (string), to (string), subject (string), date (string), ...

#### gmail.list [connector.messaging]
List emails from Gmail
Required: (none)
Optional: credential (string, default:'google'), query (any), label_ids (any), max_results (integer, default:10), include_spam_trash (boolean, default:False)
Output: messages (array), count (integer), next_page_token (any)

#### gmail.send [connector.messaging]
Send an email via Gmail
Required: to (any), subject (string), body (string)
Optional: credential (string, default:'google'), cc (any), bcc (any), content_type (string, default:'text')
Output: message_id (string), thread_id (string), label_ids (array)

#### slack.interactive_message [connector.messaging]
Send an interactive message with buttons for approval workflows
Required: channel (string), text (string), actions (array)
Optional: credential (string, default:'slack'), header (any), body (any), blocks (any), timeout_hours (any, default:48)
Output: suspend (boolean), suspend_reason (string), approval_id (string), channel (string), ts (string), actions (array)

#### slack.post_message [connector.messaging]
Post a message to a Slack channel
Required: channel (string), text (string)
Optional: credential (string, default:'slack'), blocks (any), thread_ts (any), unfurl_links (boolean, default:True), unfurl_media (boolean, default:True)
Output: ok (boolean), channel (string), ts (string), message (object)

### Connector - Productivity
*Productivity tools - Notion, Trello, Google Sheets, Airtable*

#### airtable.append_rows [connector.productivity]
Append rows to an Airtable table
Required: base_id (string), table_name (string), data (array)
Optional: credential (string, default:'airtableTokenApi')
Output: base_id (string), table_name (string), created_records (integer), record_ids (array)

#### google_docs.create [connector.productivity]
Create a new Google Doc
Required: title (string)
Optional: credential (string, default:'google')
Output: document_id (string), title (string), document_link (string)

#### google_docs.get [connector.productivity]
Get content from a Google Doc
Required: (none)
Optional: credential (string, default:'google'), document_id (any), document_url (any)
Output: document_id (string), title (string), content (string), revision_id (string)

#### google_docs.update [connector.productivity]
Update a Google Doc
Required: operation (string)
Optional: credential (string, default:'google'), document_id (any), document_url (any), text (any), find_text (any), replace_text (any), match_case (boolean, default:False)
Output: document_id (string), success (boolean), operation (string), occurrences_replaced (any)

#### google_drive.create_folder [connector.productivity]
Create a folder in Google Drive
Required: name (string)
Optional: credential (string, default:'google'), parent_folder_id (any)
Output: folder_id (string), name (string), web_view_link (string)

#### google_drive.download [connector.productivity]
Download a file from Google Drive
Required: (none)
Optional: credential (string, default:'google'), file_id (any), file_url (any), mime_type (any)
Output: file_id (string), file_name (string), mime_type (string), content (string), size (integer)

#### google_drive.get [connector.productivity]
Get file metadata from Google Drive
Required: (none)
Optional: credential (string, default:'google'), file_id (any), file_url (any), fields (any)
Output: file_id (string), name (string), mime_type (string), size (any), created_time (string), modified_time (string), ...

#### google_drive.list [connector.productivity]
List files and folders in Google Drive
Required: (none)
Optional: credential (string, default:'google'), query (any), page_size (integer, default:10), page_token (any), order_by (any), fields (any), include_trashed (boolean, default:False)
Output: files (array), count (integer), next_page_token (any)

#### google_drive.upload [connector.productivity]
Upload a file to Google Drive
Required: name (string), content (string)
Optional: credential (string, default:'google'), parent_folder_id (any), mime_type (any), is_base64 (boolean, default:False)
Output: file_id (string), name (string), mime_type (string), size (string), web_view_link (string)

#### google_sheets.append_rows [connector.productivity]
Append rows to a Google Sheet
Required: data (array)
Optional: credential (string, default:'google'), spreadsheet_id (any), spreadsheet_url (any), sheet_name (string, default:'Sheet1'), value_input_option (string, default:'USER_ENTERED'), insert_data_option (string, default:'INSERT_ROWS')
Output: spreadsheet_id (string), updated_range (string), updated_rows (integer), updated_cells (integer)

#### google_sheets.create [connector.productivity]
Create a new Google Spreadsheet
Required: title (string)
Optional: credential (string, default:'google'), sheet_names (any)
Output: spreadsheet_id (string), title (string), spreadsheet_url (string), sheets (array)

#### google_sheets.get [connector.productivity]
Get data from a Google Spreadsheet
Required: range (string)
Optional: credential (string, default:'google'), spreadsheet_id (any), spreadsheet_url (any), major_dimension (string, default:'ROWS'), value_render_option (string, default:'FORMATTED_VALUE'), include_headers (boolean, default:True)
Output: spreadsheet_id (string), range (string), values (array), row_count (integer), column_count (integer)

#### notion.append_blocks [connector.productivity]
Append child blocks to a Notion page or block
Required: block_id (string), blocks (array)
Optional: credential (string, default:'notion')
Output: results (array)

#### notion.create_page [connector.productivity]
Create a page in a Notion database
Required: database_id (string), properties (object)
Optional: credential (string, default:'notion'), content (any), icon (any), cover (any)
Output: id (string), url (string), created_time (string)

#### notion.get_database [connector.productivity]
Get a Notion database schema and metadata
Required: database_id (string)
Optional: credential (string, default:'notion')
Output: id (string), title (string), description (string), url (string), properties (object), created_time (string), ...

#### notion.get_page [connector.productivity]
Get a Notion page by ID
Required: page_id (string)
Optional: credential (string, default:'notion')
Output: id (string), url (string), created_time (string), last_edited_time (string), properties (object)

#### notion.query_database [connector.productivity]
Query entries from a Notion database
Required: database_id (string)
Optional: credential (string, default:'notion'), filter (any), sorts (any), page_size (integer, default:100), start_cursor (any)
Output: results (array), has_more (boolean), next_cursor (any), total_count (integer)

#### notion.update_page [connector.productivity]
Update a Notion page's properties
Required: page_id (string)
Optional: credential (string, default:'notion'), properties (any), icon (any), cover (any), archived (any)
Output: id (string), url (string), last_edited_time (string)

#### trello.create_card [connector.productivity]
Create a card in a Trello board
Required: list_id (string), name (string)
Optional: credential (string, default:'trello'), desc (any), pos (string, default:'bottom'), due (any), labels (any), members (any)
Output: id (string), name (string), short_url (string), url (string), list_id (string), board_id (string)

### Connector - Developer
*Developer tools - GitHub, GitLab, Jira*

#### github.get_issues [connector.developer]
Get issues and pull requests from a GitHub repository
Required: owner (string), repo (string)
Optional: credential (string, default:'github'), state (string, default:'open'), labels (any), assignee (any), creator (any), sort (string, default:'created'), direction (string, default:'desc'), per_page (integer, default:30), ... (+2 more)
Output: issues (array), total_count (integer), has_more (boolean)

### Connector - AI
*AI services for chat, image generation, and analysis.*

#### assemblyai.transcribe [connector.ai]
语音转文字 + 说话人识别 (AssemblyAI)
Required: audio_url (string)
Optional: language_code (any), speaker_labels (boolean, default:True), speakers_expected (any)
Output: text (string), utterances (array), speakers (array), confidence (any), audio_duration (any)

#### claude.chat [connector.ai]
Generate text using Claude Chat API. Use for summarization, content generation, analysis, and AI-powered text processing.
Required: prompt (string), api_key (string)
Optional: system_prompt (any), model (string, default:'claude-sonnet-4-5-20250929'), temperature (number, default:0.7), max_tokens (any), base_url (any), response_format (string, default:'text'), image_url (any)
Output: content (string), model (string), tokens (integer), finish_reason (string)

#### gemini.chat [connector.ai]
Generate text using Gemini Chat API. Use for summarization, content generation, analysis, and AI-powered text processing.
Required: prompt (string), api_key (string)
Optional: system_prompt (any), model (string, default:'gemini-2.0-flash'), temperature (number, default:0.7), max_tokens (any), base_url (any), response_format (string, default:'text'), image_url (any)
Output: content (string), model (string), tokens (integer), finish_reason (string)

#### gemini.image_edit [connector.ai]
Edit images using Gemini (style transfer, filters, artistic effects)
Required: image_url (any), prompt (string), api_key (string)
Optional: base_url (string, default:'https://api.nuwaapi.com/v1'), model (string, default:'gemini-2.5-flash-image-preview')
Output: urls (array), original_urls (any)

#### gemini.video [connector.ai]
Generate videos from text using Gemini Veo
Required: prompt (string), api_key (string)
Optional: base_url (string, default:'https://api.nuwaapi.com/v1'), model (string, default:'veo3.1-components'), aspect_ratio (string, default:'16:9'), duration_seconds (integer, default:5)
Output: url (string)

#### gemini.video_analysis [connector.ai]
Analyze video content using Gemini via OpenAI-compatible API
Required: video_url (string), prompt (string)
Optional: api_key (any), base_url (any), model (string, default:'gemini-2.0-flash'), max_tokens (any), temperature (number, default:0.7)
Output: content (string), model (string), tokens (object), finish_reason (string)

#### openai.image [connector.ai]
Generate images using OpenAI-compatible API (DALL-E, Gemini, etc.). Supports multiple models, sizes, and HD quality. Use for creating visual content, mockups, and illustrations.
Required: prompt (string), api_key (string)
Optional: base_url (any), size (string, default:'1024x1024'), quality (string, default:'standard'), n (integer, default:1), model (string, default:'dall-e-3'), response_format (string, default:'auto')
Output: url (string), revised_prompt (any)

#### openai_chat [connector.ai]
Generate text using OpenAI Chat API (GPT-4, GPT-3.5). Use for summarization, content generation, analysis, and AI-powered text processing.
Required: prompt (string), api_key (string)
Optional: system_prompt (any), model (string, default:'gpt-4o-mini'), temperature (number, default:0.7), max_tokens (any), base_url (any), response_format (string, default:'text'), image_url (any)
Output: content (string), model (string), tokens (integer), finish_reason (string)

#### xfyun.transcribe [connector.ai]
语音转文字 + 说话人识别 (讯飞开放平台)
Required: audio_url (string)
Optional: language (string, default:'cn'), role_type (integer, default:1), role_num (any)
Output: text (string), utterances (array), speakers (array), duration (any), order_id (any)
