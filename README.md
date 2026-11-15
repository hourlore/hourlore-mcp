# Hourlore MCP Server & Agent Skill

Remote Model Context Protocol (MCP) server and Agent Skill for **[Hourlore](https://hourlore.com)** — turn a single topic line into a free documentary storyboard preview or a full 5–15 minute narrated 1080p MP4 documentary with Wikimedia Commons archival imagery, animated maps, number cards and word-by-word captions.

- **MCP endpoint (Streamable HTTP):** `https://hourlore.com/mcp`
- **Authentication:** `Authorization: Bearer hl_...` (create an API key at [hourlore.com/account](https://hourlore.com/account))
- **MCP setup guide:** https://hourlore.com/docs/mcp
- **REST API reference:** https://hourlore.com/docs/api

---

## Quick Setup

1. Sign in at [hourlore.com/account](https://hourlore.com/account) and create an API key (`hl_...`).
2. Export your key:
   ```bash
   export HOURLORE_API_KEY="hl_..."
   ```

### Claude Code

```bash
claude mcp add --transport http hourlore https://hourlore.com/mcp \
  --header "Authorization: Bearer $HOURLORE_API_KEY"
```

### Cursor / Claude Desktop / Windsurf (`mcp.json`)

```json
{
  "mcpServers": {
    "hourlore": {
      "type": "http",
      "url": "https://hourlore.com/mcp",
      "headers": {
        "Authorization": "Bearer ${HOURLORE_API_KEY}"
      }
    }
  }
}
```

### OpenAI Codex CLI (`~/.codex/config.toml`)

```toml
[mcp_servers.hourlore]
url = "https://hourlore.com/mcp"
bearer_token_env_var = "HOURLORE_API_KEY"
```

---

## Available MCP Tools

| Tool | Cost | Description |
| --- | --- | --- |
| `create_storyboard_preview` | Free (daily limit) | Research a topic on Wikipedia and generate an 8–12 shot opening storyboard with script, Creative Commons archive images, maps and number cards (~25s). |
| `create_documentary_film` | 25 / 50 / 75 credits | Queue a full 5, 10 or 15 minute 1080p (16:9) narrated MP4 documentary (`olivia` or `owen` voice). |
| `get_documentary_film` | Free | Poll documentary status (optional `wait_seconds` 0–50) and retrieve the 1-hour signed MP4 `download_url` plus Wikimedia Commons attribution text. |
| `cancel_documentary_film` | Free | Cancel a queued documentary before rendering begins and release held credits back to your account. |
| `get_credits` | Free | Check available and held credits on your Hourlore account (`5 credits = 1 finished minute`). |

---

## Agent Skill (`skills/hourlore/SKILL.md`)

This repository also includes a portable `SKILL.md` for Claude Code, Cursor, Codex and Skills directories under [`skills/hourlore/SKILL.md`](skills/hourlore/SKILL.md).

## Support

Questions or feedback: [support@hourlore.com](mailto:support@hourlore.com)
