# Nodie Vault — Supported Providers

## OAuth Providers (Token-based, auto-refresh)

| Provider | Display Name | Services Covered |
|----------|-------------|-----------------|
| `google` | Google | Gmail, Google Sheets, Google Docs, Google Drive, YouTube — unified OAuth token managed by Nango |

## Composite Providers (API Key / Token)

| Provider | Display Name | Description |
|----------|-------------|-------------|
| `openai` | OpenAI | OpenAI API key with optional custom base_url endpoint |
| `slack` | Slack | Slack bot token (xoxb-...) for posting messages and interactive workflows |
| `github` | GitHub | GitHub Personal Access Token for issues, repos, and PRs |
| `notion` | Notion | Notion Integration Token (secret_...) for pages, databases, and content |
| `trello` | Trello | Trello API key + token for boards, lists, and cards |
| `airtableTokenApi` | Airtable | Airtable Personal Access Token for bases and tables |
| `smtp` | SMTP Email | SMTP credentials (host, port, username, password) for sending emails |
| `product_hunt` | Product Hunt | Product Hunt Developer Token for accessing the PH API |
| `apify` | Apify | Apify API Token for running actors and scrapers (user-level) |
| `google_service_account` | Google (Service Account) | Google Service Account JSON key for server-to-server Workspace API access |
| `supabase` | Supabase | Supabase project URL, anon key, and optional service role key |
| `reddit` | Reddit | RapidAPI key for Reddit data access via reddit3 API |

## Provider-to-Node Mapping

When a workflow node uses a `credential` parameter, it references one of the providers above. Here's the mapping:

| Node Type | Default Credential | Provider |
|-----------|-------------------|----------|
| `gmail.*` | `google` | Google (OAuth) |
| `google_sheets.*` | `google` | Google (OAuth) |
| `google_docs.*` | `google` | Google (OAuth) |
| `google_drive.*` | `google` | Google (OAuth) |
| `slack.*` | `slack` | Slack |
| `notion.*` | `notion` | Notion |
| `github.*` | `github` | GitHub |
| `trello.*` | `trello` | Trello |
| `airtable.*` | `airtableTokenApi` | Airtable |
| `email.send` | `smtp` | SMTP Email |
| `supabase.*` | `supabase` | Supabase |

## Notes

- **System-only providers** (`apify_system`, `rapidapi`) are used internally by the engine and are not exposed to users. Nodes like `twitter.search`, `youtube.search`, `instagram.*`, and `xhs.*` use system credentials automatically.
- **AI nodes** (`openai_chat`, `claude.chat`, `gemini.chat`, etc.) accept API keys directly via `$env["API_KEY"]` params — they do NOT use the credential system.
- **OAuth vs Composite**: OAuth providers handle token refresh automatically. Composite providers store static API keys/tokens that the user manages.
