---
name: nodie-credentials
description: Retrieve OAuth tokens and API keys from Nodie Vault for calling third-party APIs directly (Google, Notion, Slack, GitHub, etc.). Use when you need auth headers for direct HTTP requests, when checking which services a user has connected, or when a task fails due to missing credentials — detects the gap and guides setup automatically.
metadata: {"openclaw": {"requires": {"env": ["NODIE_API_URL", "NODIE_API_KEY"]}, "primaryEnv": "NODIE_API_KEY"}, "version": "1.0.0"}
---

# Nodie Credentials — Credential Management for Nodie Vault

## Setup

1. Create a free account at [nodie.ai](https://nodie.ai) (if you haven't already)
2. Go to **Settings → Account → Developer API** and generate your API Key
3. Configure OpenClaw with the same key used for the `nodie` skill:

```json
// ~/.openclaw/openclaw.json — add to skills.entries
{
  "nodie-credentials": {
    "enabled": true,
    "apiKey": "YOUR_API_KEY",
    "env": { "NODIE_API_URL": "https://api.nodie.ai" }
  }
}
```

This skill is the **companion to the `nodie` skill** — it enables OAuth-based integrations (Google, Notion, Slack, etc.) that the workflow engine needs. Both skills share the same API key.

## When to Use

Use this skill when:
- You want to **call a third-party API directly** (Gmail, Notion, Slack, GitHub, etc.) and need auth headers/tokens
- You need to **verify credentials before running a Nodie workflow** (pre-check that required services are connected)
- The user asks "what services are connected" or "show me my credentials"
- A workflow or task fails because of missing/expired credentials
- The user wants to set up or connect a new service

> **Key concept**: Nodie Vault is a unified credential store. Credentials retrieved here can be used in two ways: (1) by OpenClaw to call third-party APIs directly, or (2) by the Nodie workflow engine automatically during workflow execution.

All API calls use the header: `Authorization: Bearer ${NODIE_API_KEY}`


## Provider Reference

Read the provider catalog to see all supported services:

```
Read file: {baseDir}/references/providers.md
```

## Core Workflow

### When You Need a Credential for a Service

**Always follow this detect → retrieve → guide flow:**

**Step 1: Try to retrieve the credential directly**

```bash
curl -s "${NODIE_API_URL}/api/v1/openclaw/credentials/credential/{provider}" \
  -H "Authorization: Bearer ${NODIE_API_KEY}"
```

- **200 response** → Credential available. Use `auth_headers` directly in your HTTP requests.
- **404 response** → Credential not connected. Proceed to Step 2.

**Step 2: Guide the user to set up the missing credential**

The 404 response includes a `connect_url` and the `type` field. The setup flow differs by provider type:

**For OAuth providers (type: "oauth")** — user must go to the URL:

1. Show the `connect_url` as a clickable link
2. Explain: "You'll be asked to sign in and authorize access"
3. Tell the user to come back and **say "done"** after completing authorization

**For API Key providers (type: "composite")** — offer TWO options:

First, get the provider schema to know what fields are needed:

```bash
curl -s "${NODIE_API_URL}/api/v1/openclaw/credentials/credential/{provider}/schema" \
  -H "Authorization: Bearer ${NODIE_API_KEY}"
```

Response example (field names are provider-specific; use the keys from `fields` in the PUT body):

```json
{
  "provider": "notion",
  "display_name": "Notion",
  "provider_type": "composite",
  "fields": {
    "api_key": {"type": "string", "secret": true, "required": true, "description": "Notion Integration Token (secret_...)", "placeholder": "secret_xxxxxxxxxxxxxxxxxxxx"}
  },
  "saveable": true
}
```

Then present the user with two choices:

- **Option 1 — Paste directly**: Ask the user to paste the API key/token right here in the chat. Once received, save it via API. **Use the exact field name(s) from GET .../schema** (e.g. Notion uses `api_key`; GitHub uses `token`):

```bash
curl -s -X PUT "${NODIE_API_URL}/api/v1/openclaw/credentials/credential/{provider}" \
  -H "Authorization: Bearer ${NODIE_API_KEY}" \
  -H "Content-Type: application/json" \
  -d '{"data": {"api_key": "secret_xxxxx"}}'
```

- **Option 2 — Use Nodie Web UI**: Show the `connect_url` as a clickable link. The user can set up the credential on the web page at their own pace.

> **Important**: Do NOT just run `open "${connect_url}"` silently. Always include the URL in your message so the user can see and click it. The `open` command may not work in all environments.

**Step 3: Wait for user confirmation, verify, and resume**

After the credential is saved (either via direct paste or web UI):

1. Re-call the `/credential/{provider}` API (Step 1) to verify the credential is now connected
2. If **verified (200)** → tell the user it's connected, then **automatically resume the original operation** that was interrupted by the missing credential. Do NOT ask the user to repeat their request.
3. If **still missing (404)** → inform the user it's not detected yet, show the URL again, and ask them to double-check

### When the User Asks About Connected Services

Call the status endpoint:

```bash
curl -s "${NODIE_API_URL}/api/v1/openclaw/credentials/status" \
  -H "Authorization: Bearer ${NODIE_API_KEY}"
```

Response structure:

```json
{
  "connected": [
    {"provider": "google", "display_name": "Google", "type": "oauth"}
  ],
  "available": [
    {"provider": "slack", "display_name": "Slack", "type": "composite"}
  ]
}
```

Present `connected` as active services and `available` as services they can set up.

### When You Need the Setup URL for a Specific Provider

```bash
curl -s "${NODIE_API_URL}/api/v1/openclaw/credentials/connect-url?provider={provider}" \
  -H "Authorization: Bearer ${NODIE_API_KEY}"
```

Returns the Nodie Web UI URL where the user can configure credentials.

## Using Retrieved Credentials

When you receive a 200 response from `/credential/{provider}`, the response looks like:

```json
{
  "provider": "google",
  "type": "oauth",
  "connected": true,
  "auth_headers": {
    "Authorization": "Bearer ya29.xxxxx"
  },
  "credential": {
    "access_token": "ya29.xxxxx"
  }
}
```

### Two Ways to Use Credentials

**Option A: OpenClaw calls third-party APIs directly**

Use `auth_headers` from the response as HTTP headers when you call the provider's API yourself. This is ideal for quick, one-off operations where building a full workflow is overkill.

```bash
# Example: Read Gmail inbox directly
curl -s "https://gmail.googleapis.com/gmail/v1/users/me/messages?maxResults=5" \
  -H "Authorization: Bearer ya29.xxxxx"

# Example: Query a Notion database directly
curl -s "https://api.notion.com/v1/databases/{db_id}/query" \
  -H "Authorization: Bearer secret_xxxxx" \
  -H "Notion-Version: 2022-06-28" \
  -X POST
```

**Option B: Run a Nodie workflow (via the `nodie` skill)**

When executing a Nodie workflow, credentials are resolved automatically by the engine — just set the `credential` parameter in the DSL node (e.g. `credential: google`). You do NOT need to fetch credentials manually for this case. Use the `nodie` skill's credential pre-check (Step 2) to verify all required credentials are connected before execution.

### Usage Rules

1. For **direct API calls (Option A)**: use `auth_headers` as HTTP headers, or use fields from `credential` as needed by the provider
2. For **Nodie workflows (Option B)**: credentials are handled by the engine — just ensure they are connected via the status API
3. For OAuth providers (type: "oauth"), tokens are auto-refreshed by Nodie Vault — always fetch fresh before use
4. For composite providers (type: "composite"), use the credential fields as documented per provider
5. **NEVER** store or cache credentials locally — always fetch fresh from the API

## Guidance Templates

Use natural, friendly language when guiding users. Adapt these templates to the context. **Always include the URL as a clickable link and tell the user what to do after completing setup.**

### OAuth Provider Not Found (e.g. Google)

> I need access to your {display_name} account to {describe_action}. Let me check...
>
> It looks like {display_name} is not connected yet. Please click the link below to authorize access:
>
> 🔗 {connect_url}
>
> You'll be asked to sign in to your {display_name} account and grant permission. Once you've completed the authorization, just tell me **"done"** and I'll verify the connection and continue automatically.

### API Key Provider Not Found (e.g. Notion, Slack)

> I need access to your {display_name} account to {describe_action}. Let me check...
>
> It looks like {display_name} is not connected yet. You can set it up in two ways:
>
> **Option 1** — Paste it here: If you already have your {field_description} (e.g. `{placeholder}`), just paste it here and I'll save it for you.
>
> **Option 2** — Set it up on the web: Click the link below to configure it on the Nodie credentials page:
> 🔗 {connect_url}
> Once you're done there, tell me **"done"**.
>
> Which would you prefer?

When the user pastes a key/token directly:

1. Save it via `PUT /credential/{provider}` with the appropriate field name from the schema
2. Verify it was saved successfully
3. Immediately resume the original operation

### Credential Verified — Auto-Resume

After the credential is confirmed connected (via paste-save or web UI):

> ✅ {display_name} is now connected! Let me continue with {describe_original_action}...

Then **immediately resume the original operation** — do NOT ask the user to repeat their request.

### Credential Still Missing — Retry

If verification still fails after the user says they're done:

> Hmm, I still can't detect the {display_name} connection. Could you double-check that you completed all the steps? Here's the link again:
>
> 🔗 {connect_url}
>
> Common issues:
> - For OAuth: make sure you clicked "Allow" / "Authorize" on the consent screen
> - For API keys: make sure you clicked "Save" after pasting the token
>
> Or if you have the token handy, you can just paste it here directly.
>
> Let me know when you've tried again.

### Status Overview

> Here's a summary of your connected services:
>
> ✅ **Connected:** {list connected providers}
> 📋 **Available to set up:** {list available providers}
>
> Would you like to connect any of these services?

### Multiple Missing Credentials

When a task requires multiple credentials and some are missing, guide the user through them **one at a time**:

> To {describe_action}, I need access to {list_all_services}. Let me check what's connected...
>
> ✅ {connected_service} — ready
> ❌ {missing_service_1} — needs setup
> ❌ {missing_service_2} — needs setup
>
> Let's start with **{missing_service_1}**. Please click the link below:
>
> 🔗 {connect_url_1}
>
> {setup_hint_1}
>
> Tell me **"done"** when you've finished, and I'll move on to {missing_service_2}.

After all credentials are connected, resume the original operation automatically.

## Important Notes

- **User identity is automatic** — the `NODIE_API_KEY` resolves to the correct user. No need for a separate user ID.
- **OAuth tokens refresh automatically** — Nodie Vault handles token refresh via Nango. Just fetch and use.
- **Composite credentials are API keys** — they don't expire unless the user rotates them.
- **System providers are hidden** — providers like `apify_system` and `rapidapi` are internal and not shown to users.
- **Always check before using** — never assume a credential is connected. Always call the API first.
- **One provider at a time** — guide users to set up one missing credential at a time to avoid confusion.
