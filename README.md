# Hermes Agent — Unraid Templates

Unraid Docker templates for [Hermes Agent](https://github.com/NousResearch/hermes-agent), a self-hosted AI agent gateway with messaging integrations (Discord, Telegram, WhatsApp, Signal, Matrix, Mattermost, SSH, and more). The container is running in gateway mode and ready to be configured for most messaging clients.

## Templates

### Hermes Agent (Official)
- **Image:** `docker.io/nousresearch/hermes-agent:latest` (official)

### Hermes Agent (Unofficial Extras)
- **Image:** `ghcr.io/aralobster/hermes-agent:fix-docker-matrix-update` (custom build)
- **Note:** Based on [NousResearch/hermes-agent/main](https://github.com/NousResearch/hermes-agent), with extra dependencies installed for Matrix and MiniMax MCP. Auto-builds when upstream updates.
- **Repo:** [Aralobster/hermes-agent](https://github.com/Aralobster/hermes-agent/tree/fix/docker-matrix-update)

### Differences

| | Official | Unofficial Extras |
|---|---|---|
| playwright | Pre-installed | Pre-installed |
| uv | **Not installed** | Pre-installed |
| matrix (pip) | **Not installed** | Pre-installed |
| markdown (pip) | **Not installed** | Pre-installed |
| Updates | upstream | Updates from [Aralobster/hermes-agent (Unofficial)](https://github.com/Aralobster/hermes-agent/tree/fix/docker-matrix-update) |

The official image includes playwright but is missing a few pip installs needed for Matrix (`-e [matrix]`, and `markdown`), as well as `uv` for use with the [MiniMax MCP](https://platform.minimax.io/docs/token-plan/mcp-guide). The Unofficial Extras image adds both and is auto-built whenever the fork's `fix/docker-matrix-update` branch syncs with upstream.

## Quick Start

You must edit two files inside the Data (internal: /opt/data/) folder of the container — the container uses `hermes gateway run` (not the interactive `hermes setup`), so there is no guided first-run walkthrough.

**1. `/opt/data/.env`** — at your mapped host path (e.g. `/mnt/user/appdata/hermes-agent/.env`):
  - Example here: [.env.example](https://raw.githubusercontent.com/NousResearch/hermes-agent/refs/heads/main/.env.example)
  - Add at minimum an LLM provider key. ([Guide](https://hermes-agent.nousresearch.com/docs/getting-started/installation#step-7-add-your-api-keys))

**2. `/opt/data/config.yaml`** — at your mapped host path (same path as the .env):
  - Let this generate after first run.
  - Configure afterwards (the same options from the `.env` take precedence in the `config.yaml`)

## Files

```
.
├── hermes-agent-official.xml  # Official image template
├── hermes-agent-unofficial-extras.xml  # Custom image template (GHCR auto-build)
└── README.md                  # This file
```

## Docs

- [Hermes Agent Docs](https://docs.hermesagent.ai/)
- [Hermes Agent GitHub](https://github.com/NousResearch/hermes-agent)
- [Fork with uv fix](https://github.com/Aralobster/hermes-agent)
