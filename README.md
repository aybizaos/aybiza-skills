# AYBIZA agent skills

Agent skills for [AYBIZA](https://aybiza.com). A skill teaches your AI agent, such as your coding assistant or AI
client, how to work with your AYBIZA workspace.

| Skill | What it does |
|---|---|
| [`aybiza`](skills/aybiza/SKILL.md) | Connects your agent to your AYBIZA workspace over MCP, to read and update CRM records, search your knowledge base and start automations |

## Install

```
npx skills add aybizaos/aybiza-skills --skill aybiza
```

Or copy `skills/aybiza/` into your agent's skills folder.

In Hermes Agent, this repository is also a plugin package (`plugin.json`, `mcp.json`). Put your AI-tool key in the
`AYBIZA_MCP_KEY` environment variable; the package itself holds no key.

## What this repository holds

Instructions in plain text only. No code runs on install, and no key or secret is stored here. You
create your own key in your AYBIZA workspace and keep it in your own client.

## Security

To report a security issue, email security@aybiza.com.
