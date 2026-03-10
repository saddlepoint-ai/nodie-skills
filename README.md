# Nodie Skills for OpenClaw

<p align="center">
  <img src="assets/nodie-skills-icon.png" alt="Nodie Skills" width="256" />
</p>

Official [Nodie](https://nodie.ai) skills for the [OpenClaw](https://openclaw.ai) agent.

**Use when** you want to:
- Scrape XiaoHongShu, X, YouTube, Instagram, TikTok, and more with zero setup
- Run GPT, Claude, or Gemini for summarization, analysis, and generation (billed through your Nodie balance)
- Connect Notion, Google Workspace, Slack, GitHub, and others via nodie-credentials (OAuth)

## Skills

| Skill | Description | Install |
|-------|-------------|---------|
| [**nodie**](./nodie/) | 50+ integrations with zero-auth social media scraping, AI nodes, and OAuth services | `clawhub install nodie` |
| [**nodie-credentials**](./nodie-credentials/) | OAuth and API key management companion skill | `clawhub install nodie-credentials` |

## Quick Start

1. **Get your API Key**: Sign up at [nodie.ai](https://nodie.ai), then go to **Settings → Account → Developer API** to generate your key.

2. **Install skills** (choose one method):

**Option A — ClawHub CLI (recommended)**:

```bash
clawhub install nodie
clawhub install nodie-credentials
```

**Option B — GitHub URL**:

Paste the repository URL directly into your OpenClaw skill settings or when prompted for a skill source:

```
https://github.com/saddlepoint-ai/nodie-skills
```

OpenClaw will automatically detect and install the skills from the repo.

**Option C — Git Clone**:

Clone directly into your OpenClaw skills directory. This lets you track updates via `git pull`:

```bash
git clone https://github.com/saddlepoint-ai/nodie-skills.git ~/.openclaw/skills/nodie-skills
```

**Option D — Manual install from ZIP**:

Download from [Releases](https://github.com/saddlepoint-ai/nodie-skills/releases) or the green **Code → Download ZIP** button, then extract and copy the skill folders:

```bash
unzip nodie-skills-main.zip
cp -r nodie-skills-main/nodie ~/.openclaw/skills/
cp -r nodie-skills-main/nodie-credentials ~/.openclaw/skills/
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

Use GPT, Claude, and Gemini family nodes for summarization, analysis, content generation, image creation, and video analysis — all billed through your Nodie balance.

### OAuth Integrations (via nodie-credentials)

Connect Notion, Google Workspace (Gmail, Sheets, Docs, Drive), Slack, GitHub, Airtable, Trello, Supabase, and SMTP email.

## Repo Structure

```
nodie-skills/
├── nodie/                     # Main workflow engine skill
│   ├── SKILL.md               # Skill definition (OpenClaw format)
│   ├── clawhub.json           # ClawHub registry metadata
│   └── references/            # Documentation for the agent
│       ├── dsl-rules.md       # Workflow DSL syntax rules
│       ├── examples.md        # Workflow examples
│       ├── node_catalog.md    # Full node reference (keywords + parameter schemas)
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

- [Nodie Lab (homepage)](https://www.nodie.ai/lab)
- [Nodie Dashboard (pricing & billing)](https://www.nodie.ai/pricing)
- [Node Reference](https://www.nodie.ai/docs/nodes)

## License

These skills are provided by Nodie (Saddlepoint AI). Usage is subject to [Nodie's Terms of Service](https://nodie.ai/terms).
