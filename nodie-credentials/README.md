# Nodie Credentials — OAuth & API Key Management for OpenClaw

Companion skill for [nodie](../nodie/). Retrieves OAuth tokens and API keys from Nodie Vault, detects missing credentials, and guides users through setup automatically.

## Install

```bash
clawhub install nodie-credentials
```

## Configuration

Add to `~/.openclaw/openclaw.json` (use the same API key as the `nodie` skill):

```json
{
  "skills": {
    "entries": {
      "nodie-credentials": {
        "enabled": true,
        "apiKey": "npk_your_api_key_here",
        "env": { "NODIE_API_URL": "https://api.nodie.ai" }
      }
    }
  }
}
```

## Supported Providers

### OAuth (auto-refresh)

- **Google** — Gmail, Google Sheets, Docs, Drive, YouTube

### API Key / Token

- OpenAI, Slack, GitHub, Notion, Trello, Airtable, SMTP Email, Product Hunt, Supabase, Feishu

See [references/providers.md](./references/providers.md) for the full provider catalog.

## How It Works

1. **Detect** — When a task needs a credential, the skill checks if it's connected
2. **Guide** — If missing, guides the user through OAuth authorization or API key setup
3. **Resume** — After credential is connected, automatically resumes the interrupted task

Credentials can be used in two ways:
- **Direct API calls** — Use retrieved `auth_headers` for one-off HTTP requests
- **Nodie workflows** — Credentials are resolved automatically by the workflow engine

## Documentation

| File | Description |
|------|-------------|
| [SKILL.md](./SKILL.md) | Full skill definition with API reference and guidance templates |
| [references/providers.md](./references/providers.md) | Supported OAuth and API key providers |

## Links

- [Nodie Homepage](https://nodie.ai)
- [Terms of Service](https://nodie.ai/terms)
