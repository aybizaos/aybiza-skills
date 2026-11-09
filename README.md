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

## Hermes Agent

In Hermes Agent 0.21.6 or newer, this repository is also a plugin package (`plugin.json`, `mcp.json`):

1. Put your AI-tool key in the `AYBIZA_MCP_KEY` environment variable of your Hermes profile. The package itself holds
   no key.
2. Run `hermes plugins install aybiza`.

### What this plugin does on your machine and on the network

- **Network.** Every tool call, with its arguments, goes to `app.aybiza.com` and acts on your AYBIZA workspace within
  the permissions of your key. The tools come from the AYBIZA server when Hermes connects.
- **Writes.** Write tools change CRM records and start automations. The package marks the server `untrusted`, so
  Hermes asks before any tool the server does not mark read-only, unless you approve that tool for the session or
  always, and refuses them in unattended runs. Some tools also need a manager's approval or a fresh second-factor
  check in your workspace.
- **Credentials.** Your AI-tool key, from `AYBIZA_MCP_KEY`. The key opens the MCP endpoint only. Email addresses and
  phone numbers arrive as placeholders unless an owner or admin allows full contact details for that key. The plugin
  reads no files and stores no tokens.
- **Nothing else.** No local code, no shell commands, no background processes, no telemetry and no self-updater.

## What this repository holds

Instructions in plain text only. No code runs on install, and no key or secret is stored here. You
create your own key in your AYBIZA workspace and keep it in your own client.

## Security

To report a security issue, email security@aybiza.com.
