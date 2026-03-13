---
name: nodie
description: Build and run automated workflows connecting 50+ services. Zero-auth social media scraping for 9 platforms (Twitter/X, YouTube, Instagram, TikTok, Pinterest, Reddit, LinkedIn, Bilibili, Discord). AI-powered nodes (GPT-4, Claude, Gemini). Connect Notion, Google Workspace, Slack and more via OAuth. Use when the user wants to automate multi-step tasks, fetch platform data, or schedule recurring jobs.
homepage: https://github.com/saddlepoint-ai/nodie-skills
metadata: {"clawdbot": {"emoji": "🤖", "requires": {"env": ["NODIE_API_URL", "NODIE_API_KEY"]}, "primaryEnv": "NODIE_API_KEY", "files": ["references/*"]}, "version": "1.0.0"}
---

# Nodie Workflow Engine

## Setup

1. Create a free account at [nodie.ai](https://nodie.ai)
2. Go to **Settings → Account → Developer API** and generate your API Key
3. Configure OpenClaw:

```json
// ~/.openclaw/openclaw.json
{
  "skills": {
    "entries": {
      "nodie": {
        "enabled": true,
        "apiKey": "YOUR_API_KEY",
        "env": { "NODIE_API_URL": "https://api.nodie.ai" }
      }
    }
  }
}
```

4. **(Strongly recommended)** Install the credential management companion skill for OAuth services (Google, Notion, Slack, etc.):

```bash
clawhub install nodie-credentials
```

Configure it with the same API key — no extra credentials needed.

Without this skill, OAuth-based nodes (~20 integrations) will not work.

## When to Use

- User wants to search/fetch content from platforms (Twitter/X, YouTube, Instagram, TikTok, Pinterest, Reddit, Bilibili, LinkedIn)
- User wants to connect multiple services in a pipeline (fetch → transform → save)
- User wants to schedule recurring automations
- User wants to generate documents/reports from external data
- User references a previously built workflow

## API Reference

All requests go to `$NODIE_API_URL` with `Authorization: Bearer $NODIE_API_KEY`.

| Action | Method | Endpoint |
|--------|--------|----------|
| Create workspace | POST | `/api/v1/openclaw/workspaces/create` |
| Save workflow DSL | POST | `/api/v1/openclaw/workspaces/{workspace_id}/save` |
| Execute workflow | POST | `/api/v1/openclaw/execute` |
| Get workflow | GET | `/api/v1/openclaw/workspaces/{workspace_id}/workflow` |
| Get execution result | GET | `/api/v1/openclaw/executions/{execution_id}` |
| List executions | GET | `/api/v1/openclaw/workspaces/{workspace_id}/executions?limit=20` |
| List workspaces | GET | `/api/v1/openclaw/workspaces/list` |
| Delete workspace | DELETE | `/api/v1/openclaw/workspaces/{workspace_id}` |

### Typical Flow

1. **Create workspace** → get `workspace_id`
2. **Save DSL** to the workspace (JSON body with workflow definition)
3. **Execute** with `{"workspaceId": workspace_id}` → get `execution_id` + results
4. **Present results** to the user

For past results: GET execution by `execution_id`.

### Execution Timing (IMPORTANT)

Many nodes rely on external services (Apify crawlers, AssemblyAI, LLM generation, etc.) and take **30–120 seconds** to complete. Never assume instant completion.

**Slow nodes** (expect 30–120s): `twitter.search`, `youtube.search`, `youtube.get_videos`, `youtube.get_channel`, `instagram.search`, `tiktok.search`, `pinterest.search`, `linkedin.search`, `reddit.search`, `video.fetch`, `assemblyai.transcribe`, `xfyun.transcribe`, `gemini.video`.

**Required pattern when calling `/execute`:**

1. **Set a long timeout on your exec/fetch call** — at least 90–120 seconds. The default shell timeout (e.g. 10s) is far too short for most workflows.
   ```
   # Example: set yieldMs/timeout to 120s
   exec(command="curl -s -m 120 -X POST ...", yieldMs=120000)
   ```
2. **If the command backgrounds** (you see "Command still running" or similar), **you MUST poll/wait for completion** before responding. Use your runtime's polling mechanism (e.g. `process(action=poll, timeout=90000)`) to block until the HTTP response is fully received.
3. **Async fallback** — if polling is unavailable, use the GET endpoint to check execution status:
   ```bash
   curl -s "$NODIE_API_URL/api/v1/openclaw/executions/{execution_id}" \
     -H "Authorization: Bearer $NODIE_API_KEY"
   ```
   Re-check every 10–15 seconds until `status` is `completed` or `failed`.
4. **NEVER report "0 results", "no data", or "execution failed"** until you have confirmed the execution has actually finished (received a complete HTTP response with status and body). A backgrounded or timed-out command is NOT a completed execution.

## Node Catalog

All available nodes are listed below. For each node you select, read its parameter schema: `{baseDir}/references/nodes/<node_type>.md`

### Triggers & Control Flow

| Node | Purpose | Auth |
|------|---------|------|
| trigger.manual | Manual trigger — entry point for all workflows | — |
| input | Pause workflow and wait for user input (multi-question forms) | — |
| if | Conditional routing based on expression | — |
| loop | Iterate over array with sub-workflow per item | — |
| code | Execute Python in sandbox (data transform, filtering, formatting) | — |
| output | Define workflow outputs (text, image, video, json, markdown, file) | — |

### Data & HTTP

| Node | Purpose | Auth |
|------|---------|------|
| http_request | Make HTTP requests (GET/POST/PUT/DELETE) to external APIs | optional credential |
| rss.read | Fetch and parse RSS/Atom feeds | — |
| storage.get | Retrieve data from S3, KV storage, or HTTP URL | — |
| storage.store | Store data to S3 or KV storage | — |
| markdown.convert | Convert between Markdown and HTML | — |

### Social Media & Search (zero-auth)

| Node | Purpose | Auth |
|------|---------|------|
| twitter.search | Search Twitter/X tweets by keyword or user | zero-auth (apify) |
| reddit.search | Search Reddit posts, subreddits, or users | zero-auth (apify) |
| youtube.search | Search YouTube videos, channels, or playlists | zero-auth (apify) |
| youtube.get_videos | Get detailed info about YouTube videos | zero-auth (apify) |
| youtube.get_channel | Get YouTube channel info | zero-auth (apify) |
| instagram.search | Search and scrape Instagram hashtags, users, or places | zero-auth (apify) |
| tiktok.search | Search TikTok by keyword or scrape profile/hashtag URLs | zero-auth (apify) |
| pinterest.search | Search Pinterest pins by keyword | zero-auth (apify) |
| linkedin.search | Search LinkedIn job postings | zero-auth (apify) |
| discord.messages | Read messages from a Discord channel | — |
| video.fetch | Get direct video URL from Bilibili, YouTube, TikTok, etc. | zero-auth |

### Messaging

| Node | Purpose | Auth |
|------|---------|------|
| email.send | Send email via SMTP (TLS/SSL, HTML, CC/BCC) | smtp credential |
| gmail.send | Send email via Gmail | google credential |
| gmail.list | List/search emails from Gmail | google credential |
| gmail.get | Get email details from Gmail | google credential |
| slack.post_message | Post a message to a Slack channel | slack credential |
| slack.interactive_message | Send interactive buttons for approval workflows | slack credential |

### Productivity

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
| trello.create_card | Create a card in a Trello board | trello credential |
| supabase.execute | CRUD operations on Supabase tables | supabase credential |
| supabase.batch | Multiple parallel Supabase queries | supabase credential |

### Developer

| Node | Purpose | Auth |
|------|---------|------|
| github.get_issues | Get issues/PRs from a GitHub repository | github credential |

### AI

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

### Not Available (do not attempt)

- `google_calendar.*` — no workflow node. For calendar access, use the `caldav` skill instead (supports iCloud, Nextcloud, Fastmail, Google Calendar via app password). As a quick read-only fallback, ask the user for their calendar's ICS/webcal URL and fetch it with `http_request`.
- `weather.*` — no weather node. Use `http_request` with a public API (e.g. Open-Meteo: `https://api.open-meteo.com/v1/forecast`) or inform the user.

## DSL Reference

Read `{baseDir}/references/dsl-rules.md` for the full DSL specification.
Read `{baseDir}/references/examples.md` for complete workflow examples.

### Quick Example

```yaml
name: Search Twitter for Coffee
nodes:
  - id: trigger_1
    type: trigger.manual
    name: Start
    params: {}
    next: [search_1]

  - id: search_1
    type: twitter.search
    name: Search Twitter
    params:
      query: "coffee shops Shanghai"
      max_items: 10
    next: [output_1]

  - id: output_1
    type: output
    name: Results
    params:
      outputs:
        - type: json
          value: $search_1
          label: "Twitter Results"
    next: []
```

Key points:
- Every workflow starts with `trigger.manual`
- Nodes connect via `next` — nodes without `next` are dead ends
- End with an `output` node to surface results
- Reference other nodes' output: `$node_id['field']` or `${{ node_id['field'] }}` for string interpolation

## Credentials

- **Zero-auth nodes** (Twitter, Reddit, YouTube, Instagram, TikTok, Pinterest, LinkedIn, video.fetch): work out of the box, no setup needed. Nodie handles all API keys.
- **OAuth nodes** (Notion, Slack, Google, GitHub, etc.): requires the `nodie-credentials` companion skill. It detects missing credentials and guides the user through OAuth authorization via the Nodie Dashboard.
- **AI nodes** (OpenAI, Claude, Gemini): managed by the Nodie platform. Usage is billed to your Nodie account balance — no need to bring your own API keys.

## Rules

1. **Wait for execution to complete before responding.** Workflow execution can take 30–120 seconds. Never interpret a backgrounded, timed-out, or incomplete HTTP call as "no results". See **Execution Timing** above.
2. **Always include `next`** between nodes. Nodes without `next` are dead ends whose output is lost.
3. **Always end with `output`** node to surface results to the user.
4. **Read node schemas** (`references/nodes/<type>.md`) before generating DSL — do NOT guess parameters.
5. **Never fabricate data** — run actual API calls and present real responses. If execution fails, report honestly.
6. **Use `$env['VAR']`** for API keys (string form only). Never use `{"$env": "VAR"}` or `$env.VAR`.
7. **Use `code` nodes** for data transformation (formatting, filtering). Use AI nodes (`openai_chat`, `claude.chat`) for analysis/summarization.
8. **No logic in `${{ }}`** — only simple path references. Complex formatting goes in a `code` node first.
9. **Message delivery**: Use `output` node for replying to the current user. Use messaging nodes (`slack.post_message`, `email.send`, etc.) only when sending to a specific external target.
10. **Never show raw workflow DSL/JSON to the user.** The workflow is internal scaffolding; present results in natural language.

## Scheduling Workflows

To schedule a workflow, use the `cron` tool to create a job that executes the workflow via the Nodie API. Always build workflows with `trigger.manual` — the cron job handles timing.

**Pattern**: save workflow → create cron job with `agentTurn` payload → isolated session calls `/api/v1/openclaw/execute` at scheduled time.

Cron payload message template:
```
Execute Nodie workflow in workspace <WORKSPACE_ID> using the nodie skill. Summarize the results and highlight anything noteworthy.
```

Use `sessionTarget: "isolated"` and `delivery: { mode: "announce" }` so results go to the user's chat without polluting main session history.

## External Endpoints

| Endpoint | Method | Data Sent |
|----------|--------|-----------|
| `$NODIE_API_URL/api/v1/openclaw/workspaces/create` | POST | Workspace name |
| `$NODIE_API_URL/api/v1/openclaw/workspaces/{id}/save` | POST | Workflow DSL (node definitions, parameters) |
| `$NODIE_API_URL/api/v1/openclaw/execute` | POST | Workspace ID |
| `$NODIE_API_URL/api/v1/openclaw/executions/{id}` | GET | — |
| `$NODIE_API_URL/api/v1/openclaw/workspaces/{id}/workflow` | GET | — |
| `$NODIE_API_URL/api/v1/openclaw/workspaces/{id}/executions` | GET | — |
| `$NODIE_API_URL/api/v1/openclaw/workspaces/list` | GET | — |
| `$NODIE_API_URL/api/v1/openclaw/workspaces/{id}` | DELETE | — |

All requests are authenticated with `Authorization: Bearer $NODIE_API_KEY`. No other external endpoints are contacted directly by this skill.

## Security & Privacy

- **What leaves your machine**: Workflow DSL definitions (node types, parameters, search keywords) and execution commands are sent to the Nodie API server (`$NODIE_API_URL`).
- **What stays local**: No local files are read or written. No local services are accessed. The skill operates entirely via HTTP API calls.
- **Credentials**: Only `NODIE_API_KEY` is used for authentication. Upstream provider keys (Apify, OpenAI, etc.) are managed server-side by Nodie and never appear on the client.
- **Data retention**: Workflow definitions and execution results are stored on the Nodie platform under your account. See [Nodie Privacy Policy](https://nodie.ai/privacy) for details.

## Model Invocation Note

This skill may be invoked autonomously by the OpenClaw agent when it determines a workflow automation task is relevant. This is standard behavior for installed skills. You can disable this skill at any time by setting `"enabled": false` in your `openclaw.json` configuration.

## Trust Statement

By installing and using this skill, workflow definitions and execution data are sent to the Nodie API (`api.nodie.ai`), operated by Saddlepoint AI. Only install this skill if you trust [Nodie](https://nodie.ai) and accept the [Nodie Terms of Service](https://nodie.ai/terms).