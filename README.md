# Hermes Agent — Unraid Templates

Unraid Docker templates for [Hermes Agent](https://github.com/NousResearch/hermes-agent), a self-hosted AI agent gateway with messaging integrations (Discord, Telegram, WhatsApp, Signal, Matrix, Mattermost, SSH, and more).

## Templates

### Hermes Agent (Official)
- **Image:** `nousresearch/hermes-agent:latest` (official, no custom modifications)
- **Best for:** Quick setup, vanilla experience, always up-to-date with upstream
- **Post Arguments:** `--gateway run`

### Hermes Agent (Full)
- **Image:** `docker.io/aralobster/hermes-agent:latest` (custom build, pre-installs dependencies)
- **Best for:** Full functionality without rebuild delays
- **Requires:** One-time custom image build (see below)
- **Post Arguments:** `--gateway run`

### Differences

| | Official | Full |
|---|---|---|
| `playwright` | Not installed | Pre-installed |
| `markdown` | Not installed | Pre-installed |
| Setup time | Slower first run | Faster first run |
| Upstream updates | Immediate | Requires rebuild |

## Quick Start — Official Template

1. Download `hermes-agent-official.xml` to `/boot/config/docker.d/` on your Unraid server
2. In the Docker UI:
   - Set **Post Arguments**: `--gateway run`
   - Add a **Config** path mapping: `/opt/data` → your host path (e.g. `/mnt/user/appdata/hermes-agent`)
3. Start the container — follow the logs for first-run setup
4. Edit `/opt/data/.env` (at your mapped host path) with your API keys and platform credentials
5. Restart the container to apply

## Full Template Setup

### 1. Build the custom image

The Full template requires a custom Docker image to be built and pushed first.

```bash
# Clone this repo
git clone https://github.com/ebears/hermes-agent-unraid.git
cd hermes-agent-unraid

# Authenticate with Docker Hub (or GHCR)
docker login

# Build and push
docker build -t docker.io/aralobster/hermes-agent:latest -f Dockerfile.unraid .
docker push docker.io/aralobster/hermes-agent:latest
```

### 2. Install the template

1. Download `hermes-agent-full.xml` to `/boot/config/docker.d/` on your Unraid server
2. In the Docker UI:
   - Set **Post Arguments**: `--gateway run`
   - Add a **Config** path mapping: `/opt/data` → your host path (e.g. `/mnt/user/appdata/hermes-agent`)
3. Start the container — follow the logs for first-run setup
4. Edit `/opt/data/.env` (at your mapped host path) with your API keys and platform credentials
5. Restart the container to apply

### Updating the Full image

When Hermes Agent releases a new version:

```bash
cd hermes-agent-unraid
docker pull nousresearch/hermes-agent:latest
docker build -t docker.io/aralobster/hermes-agent:latest -f Dockerfile.unraid .
docker push docker.io/aralobster/hermes-agent:latest
```

Then in Unraid, set the container to pull the latest image.

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
