# Changelog

All notable changes to the Nodie Skills for OpenClaw will be documented in this file.

## [1.0.0] - 2026-03-10

### Added

- **nodie** skill: Workflow automation engine with 60+ node types
  - Zero-auth social media scraping: XHS, Twitter/X, YouTube, Instagram, TikTok, Pinterest, Reddit, LinkedIn, Bilibili, Discord
  - AI-powered nodes: GPT-4, Claude, Gemini (chat, image, video generation/analysis)
  - OAuth integrations: Google Workspace, Notion, Slack, GitHub, Airtable, Trello, Supabase, Feishu
  - Control flow: conditional routing, loops, code sandbox, user input forms
  - Data nodes: HTTP requests, RSS, storage (S3/KV), markdown conversion
  - Full DSL specification with YAML workflow definitions
  - Per-node parameter documentation (60+ reference files)
  - Workflow examples (RSS→Slack, social media research, multi-step pipelines)
- **nodie-credentials** skill: Companion credential management
  - OAuth token retrieval with auto-refresh (Google)
  - API key management for 10+ providers
  - Automatic missing-credential detection and guided setup flow
  - Direct API call support via retrieved auth headers
- ClawHub metadata and security documentation for both skills
