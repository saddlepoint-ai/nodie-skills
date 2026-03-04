# Nodie Skills for OpenClaw

Official [OpenClaw](https://openclaw.ai) skills for the [Nodie](https://nodie.ai) workflow automation platform.

## Skills

| Skill | Description | Install |
|-------|-------------|---------|
| [**nodie**](./nodie/) | 50+ integrations with zero-auth social media scraping, AI nodes, and OAuth services | `clawhub install nodie` |
| [**nodie-credentials**](./nodie-credentials/) | OAuth and API key management companion skill | `clawhub install nodie-credentials` |

## Quick Start

1. **Get your API Key**: Sign up at [nodie.ai](https://nodie.ai), then go to **Settings → Account → Developer API** to generate your key.

2. **Install skills**:

```bash
clawhub install nodie
clawhub install nodie-credentials
```

3. **Configure** `~/.openclaw/openclaw.json`:

```json
{
  "skills": {
    "entries": {
      "nodie": {
        "enabled": true,
        "apiKey": "npk_your_api_key_here",
        "env": { "NODIE_API_URL": "https://api.nodie.ai" }
      },
      "nodie-credentials": {
        "enabled": true,
        "apiKey": "npk_your_api_key_here",
        "env": { "NODIE_API_URL": "https://api.nodie.ai" }
      }
    }
  }
}
```

4. **Start using**: Ask your OpenClaw agent to search social media, build workflows, or connect services.

## What Can You Do?

### Zero-Auth Social Media (no setup needed)

Search and scrape content from XiaoHongShu (RedNote), Twitter/X, YouTube, Instagram, TikTok, Pinterest, Reddit, LinkedIn, Bilibili, and Discord.

### AI-Powered Processing

Use GPT-4, Claude, and Gemini nodes for summarization, analysis, content generation, image creation, and video analysis — all billed through your Nodie balance.

### OAuth Integrations (via nodie-credentials)

Connect Notion, Google Workspace (Gmail, Sheets, Docs, Drive), Slack, GitHub, Airtable, Trello, Supabase, and SMTP email.

### Scheduling

Combine with OpenClaw's cron tool to schedule recurring workflow executions.

## Repo Structure

```
nodie-skills/
├── nodie/                     # Main workflow engine skill
│   ├── SKILL.md               # Skill definition (OpenClaw format)
│   ├── clawhub.json           # ClawHub registry metadata
│   └── references/            # Documentation for the agent
│       ├── dsl-rules.md       # Workflow DSL syntax rules
│       ├── examples.md        # Workflow examples
│       ├── node_catalog.md    # Node quick reference
│       ├── node_catalog_full.generated.md  # Auto-generated full catalog
│       └── nodes/             # Per-node detailed docs (60+ files)
├── nodie-credentials/         # Credential management companion skill
│   ├── SKILL.md
│   ├── clawhub.json
│   └── references/
│       └── providers.md       # Supported OAuth providers
└── README.md
```

## Billing

All usage (social media scraping, AI calls, etc.) is billed through your Nodie account balance. New accounts receive free credits. Top up via the Nodie Dashboard billing page.

## Contributing

We welcome issues and feature requests. For skill improvements, please open a pull request.

## Support

- [Nodie Dashboard](https://nodie.ai)
- [Node Reference](https://www.nodie.ai/docs/nodes)

## License

These skills are provided by Nodie (Saddlepoint AI). Usage is subject to [Nodie's Terms of Service](https://nodie.ai/terms).
