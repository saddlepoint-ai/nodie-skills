# Nodie — Workflow Automation Skill for OpenClaw

Build and run automated workflows connecting 50+ services from your OpenClaw agent.

## Highlights

- **Zero-auth social media scraping**: XiaoHongShu, Twitter/X, YouTube, Instagram, TikTok, Pinterest, Reddit, LinkedIn, Bilibili, Discord — no API keys needed
- **AI-powered nodes**: GPT-4, Claude, Gemini for summarization, analysis, content generation, image creation, and video analysis
- **OAuth integrations**: Notion, Google Workspace (Gmail, Sheets, Docs, Drive), Slack, GitHub, Airtable, Trello, Supabase (requires companion skill `nodie-credentials`)
- **60+ node types** with full parameter documentation

## Install

```bash
clawhub install nodie
```

## Configuration

Add to `~/.openclaw/openclaw.json`:

```json
{
  "skills": {
    "entries": {
      "nodie": {
        "enabled": true,
        "apiKey": "npk_your_api_key_here",
        "env": { "NODIE_API_URL": "https://api.nodie.ai" }
      }
    }
  }
}
```

Get your API key at [nodie.ai](https://nodie.ai) → **Settings → Account → Developer API**.

## Companion Skill

Install [nodie-credentials](../nodie-credentials/) for OAuth-based integrations (Google, Notion, Slack, etc.):

```bash
clawhub install nodie-credentials
```

Without it, ~20 OAuth-dependent nodes will not work.

## Documentation

| File | Description |
|------|-------------|
| [SKILL.md](./SKILL.md) | Full skill definition with API reference, node catalog, DSL rules |
| [references/dsl-rules.md](./references/dsl-rules.md) | Workflow DSL syntax specification |
| [references/examples.md](./references/examples.md) | Complete workflow examples |
| [references/node_catalog.md](./references/node_catalog.md) | All nodes with parameter schemas |
| [references/nodes/](./references/nodes/) | Per-node detailed documentation (60+ files) |

## Billing

All usage (social media scraping, AI calls, etc.) is billed through your Nodie account balance. New accounts receive free credits. Top up at [nodie.ai/pricing](https://nodie.ai/pricing).

## Links

- [Nodie Homepage](https://nodie.ai)
- [Node Reference](https://nodie.ai/docs/nodes)
- [Terms of Service](https://nodie.ai/terms)
