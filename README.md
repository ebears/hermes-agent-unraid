# Hermes Agent — Unraid Templates

Unraid Docker templates for [Hermes Agent](https://github.com/NousResearch/hermes-agent), a self-hosted AI agent gateway with messaging integrations (Discord, Telegram, WhatsApp, Signal, Matrix, Mattermost, SSH, and more).

## Templates

### Hermes Agent (Official)
- **Image:** `nousresearch/hermes-agent:latest` (official, no custom modifications)
- **Best for:** Quick setup, vanilla experience, always up-to-date with upstream
- **Post Arguments:** `--gateway run`

### Hermes Agent (Full)
- **Image:** `ghcr.io/Aralobster/hermes-agent:fix/docker-matrix-update` (auto-built from fork)
- **Best for:** Full functionality, auto-updates when upstream changes
- **Post Arguments:** `--gateway run`

### Differences

| | Official | Full |
|---|---|---|
| `playwright` | Not installed | Pre-installed |
| `markdown` | Not installed | Pre-installed |
| `uv` | Not installed | Pre-installed |
| Setup time | Slower first run | Faster first run |
| Upstream updates | Immediate | Auto-built on push to fix/docker-matrix-update |

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
├── Dockerfile.unraid          # Builds the custom image for Full template
├── hermes-agent-official.xml  # Official image template
├── hermes-agent-full.xml     # Custom image template
├── README.md                  # This file
└── hermes-icon.png           # App icon (add your own at this path)
```

## Docs

- [Hermes Agent Docs](https://docs.hermesagent.ai/)
- [Hermes Agent GitHub](https://github.com/NousResearch/hermes-agent)
- [Fork with Unraid fixes](https://github.com/Aralobster/hermes-agent)
