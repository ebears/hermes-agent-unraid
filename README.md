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
| markdown | Pre-installed (upstream) | Pre-installed (upstream) |
| uv | **Not installed** | Pre-installed |
| Auto-updates | With official upstream | **Auto-built on push to fix/docker-matrix-update** |

The official image already includes playwright and markdown from the upstream Dockerfile. The Full image additionally includes `uv` (needed for MCP `uvx` commands) and is auto-built whenever the fork's `fix/docker-matrix-update` branch updates.

## Quick Start — Official Template

1. Download `hermes-agent-official.xml` to `/boot/config/docker.d/` on your Unraid server
2. In the Docker UI:
   - Set **Post Arguments**: `--gateway run`
   - Add a **Config** path mapping: `/opt/data` → your host path (e.g. `/mnt/user/appdata/hermes-agent`)
3. Start the container — follow the logs for first-run setup
4. Edit `/opt/data/.env` (at your mapped host path) with your API keys and platform credentials
5. Restart the container to apply

## Full Template Setup

The Full template pulls from a GHCR image that is auto-built from the
[fix/docker-matrix-update](https://github.com/Aralobster/hermes-agent/tree/fix/docker-matrix-update) branch
whenever it updates.

To update: push to the `fix/docker-matrix-update` branch on the
[Aralobster/hermes-agent](https://github.com/Aralobster/hermes-agent) fork, then
set the container to pull the latest image in the Docker UI.

1. Download `hermes-agent-full.xml` to `/boot/config/docker.d/` on your Unraid server
2. In the Docker UI:
   - Set **Post Arguments**: `--gateway run`
   - Add a **Config** path mapping: `/opt/data` → your host path (e.g. `/mnt/user/appdata/hermes-agent`)
3. Start the container — follow the logs for first-run setup
4. Edit `/opt/data/.env` (at your mapped host path) with your API keys and platform credentials
5. Restart the container to apply

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
