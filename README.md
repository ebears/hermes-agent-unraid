# Hermes Agent — Unraid Templates

Unraid Docker templates for [Hermes Agent](https://github.com/NousResearch/hermes-agent), a self-hosted AI agent gateway with messaging integrations (Discord, Telegram, WhatsApp, Signal, Matrix, Mattermost, SSH, and more).

## Templates

### Hermes Agent (Official)
- **Image:** `docker.io/nousresearch/hermes-agent:latest` (official)
- **Best for:** Quick setup, vanilla experience, always up-to-date with upstream
- **Post Arguments:** `--gateway run`

### Hermes Agent (Full)
- **Image:** `ghcr.io/aralobster/hermes-agent:fix-docker-matrix-update` (custom build)
- **Best for:** Full functionality with upstream, auto-builds when upstream updates
- **Post Arguments:** `--gateway run`
- **Built from:** [Aralobster/hermes-agent](https://github.com/Aralobster/hermes-agent/tree/fix/docker-matrix-update)

### Differences

| | Official | Full |
|---|---|---|
| playwright | Pre-installed (upstream) | Pre-installed (upstream) |
| markdown | **Not installed** | Pre-installed |
| uv | **Not installed** | Pre-installed |
| Setup time | Faster first run | Slower first run (more layers) |
| Upstream updates | Immediate | Auto-built on push to fix/docker-matrix-update |

The official image includes playwright but is missing `markdown` and `uv`. The Full image adds both (needed for Matrix HTML rendering and MCP via `uvx`) and is auto-built whenever the fork's `fix/docker-matrix-update` branch syncs with upstream.

## Quick Start — Official Template

### Before you start

You must create two files **before** running the container for the first time — the container uses `hermes gateway run` (not the interactive `hermes setup`), so there is no guided first-run walkthrough.

**1. `/opt/data/.env`** — at your mapped host path (e.g. `/mnt/user/appdata/hermes-agent/.env`):
```
# Required: your LLM provider API key
MINIMAX_API_KEY=***

# Optional: provider model override
# MINIMAX_MODEL=***

# Matrix credentials (if using Matrix)
MATRIX_HOMESERVER=https://matrix.yourdomain.com
MATRIX_ACCESS_TOKEN=***
MATRIX_USER_ID=@youruser:matrix.yourdomain.com
```

**2. `/opt/data/config.yaml`** — at your mapped host path:
```yaml
display:
  skin: default

platforms:
  matrix:
    enabled: true
```

### Install

1. Download `hermes-agent-official.xml` to `/boot/config/docker.d/` on your Unraid server
2. In the Docker UI:
   - Set **Post Arguments**: `--gateway run`
   - Add a **Config** path mapping: `/opt/data` → your host path (e.g. `/mnt/user/appdata/hermes-agent`)
3. Start the container
4. Monitor logs with `docker logs hermes-agent` — if it crashes, your `.env` or `config.yaml` is misconfigured
5. Once running without errors, send a message to your Matrix bot user ID to verify the connection

## Full Template Setup

The Full template pulls from a GHCR image that is auto-built from the
[fix/docker-matrix-update](https://github.com/Aralobster/hermes-agent/tree/fix/docker-matrix-update) branch
whenever it updates.

To update: push to the `fix/docker-matrix-update` branch on the
[Aralobster/hermes-agent](https://github.com/Aralobster/hermes-agent) fork, then
set the container to pull the latest image in the Docker UI.

### Before you start

You must create two files **before** running the container for the first time — the container uses `hermes gateway run` (not the interactive `hermes setup`), so there is no guided first-run walkthrough.

**1. `/opt/data/.env`** — at your mapped host path (e.g. `/mnt/user/appdata/hermes-agent/.env`):
```
# Required: your LLM provider API key
MINIMAX_API_KEY=***

# Optional: provider model override
# MINIMAX_MODEL=***

# Matrix credentials (if using Matrix)
MATRIX_HOMESERVER=https://matrix.yourdomain.com
MATRIX_ACCESS_TOKEN=***
MATRIX_USER_ID=@youruser:matrix.yourdomain.com
```

**2. `/opt/data/config.yaml`** — at your mapped host path:
```yaml
display:
  skin: default

platforms:
  matrix:
    enabled: true
```

### Install

1. Download `hermes-agent-full.xml` to `/boot/config/docker.d/` on your Unraid server
2. In the Docker UI:
   - Set **Post Arguments**: `--gateway run`
   - Add a **Config** path mapping: `/opt/data` → your host path (e.g. `/mnt/user/appdata/hermes-agent`)
3. Start the container
4. Monitor logs with `docker logs hermes-agent` — if it crashes, your `.env` or `config.yaml` is misconfigured
5. Once running without errors, send a message to your Matrix bot user ID to verify the connection

## Community Apps Submission

Both templates can be submitted to [Unraid Community Apps](https://forums.unraid.net/forum/83/community-apps/).

1. Create a thread in the Community Apps forum
2. Include the XML files and a brief description
3. Follow the [CA submission guidelines](https://forums.unraid.net/topic/89926-community-applications-repository-requirements/)

## Files

```
.
├── hermes-agent-official.xml  # Official image template
├── hermes-agent-full.xml     # Custom image template (GHCR auto-build)
└── README.md                  # This file
```

## Docs

- [Hermes Agent Docs](https://docs.hermesagent.ai/)
- [Hermes Agent GitHub](https://github.com/NousResearch/hermes-agent)
- [Fork with uv fix](https://github.com/Aralobster/hermes-agent)
