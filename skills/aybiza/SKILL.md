---
name: aybiza
description: Connect an AI agent to an AYBIZA workspace over MCP, so it can read and update CRM records, search the knowledge base, and start automations for the user's business. Use when the user mentions AYBIZA, asks to work with their AYBIZA contacts, deals, tickets, calls or knowledge, or wants their coding assistant or AI client connected to AYBIZA.
---

# AYBIZA

AYBIZA runs a business's calls, chats, records and automations with AI agents. This skill connects
you, the agent, to the user's own AYBIZA workspace. Once connected, you can read and update their CRM,
search their knowledge base, and start their automations, inside the permissions they give you.

## When to use

- The user asks about their AYBIZA contacts, deals, tickets, calls or knowledge.
- The user wants to create or update a record in AYBIZA from their editor or AI client.
- The user asks you to connect their AI tool to AYBIZA.

## Connect

There are two ways. Ask the user which one their client supports.

**1. Sign in with OAuth (no key).** Give the client this address:

```
https://app.aybiza.com/mcp
```

The client opens a page in the browser and the user approves it. Tell the user to be signed in to
`app.aybiza.com` in that browser first.

**2. An AI-tool key.** The user creates the key, never you. Tell them:

> In your AYBIZA workspace at app.aybiza.com, ask AY for a key for your AI tool, or tick
> "For an AI tool: MCP only" in the key builder. Pick only the permissions this tool needs.

The key starts with `aybiza-mcp_`. It opens the MCP endpoint and nothing else. Most clients take a
server entry like this:

```json
{
  "mcpServers": {
    "aybiza": {
      "url": "https://app.aybiza.com/api/v1/mcp",
      "headers": {
        "x-api-key": "${AYBIZA_MCP_KEY}"
      }
    }
  }
}
```

Here the key comes from an environment variable named `AYBIZA_MCP_KEY`. If the client cannot read
environment variables in its config, keep the key in its own secret store. Never write the key into a
file you commit, never print it back, and never paste it into chat.

## Work

1. **Ask what you can do.** Call `tools/list` first. The answer is the truth for this key: it lists
   only the tools the key's permissions cover, with the arguments each one takes. Do not guess tool
   names or work from an old list.
2. **Read before you write.** Look a record up before you change it, and show the user what you
   found.
3. **Confirm every change.** Before you create, update or delete anything, say what will change and
   wait for the user's yes.
4. **Respect the answer.** Some tools need a manager's approval or a fresh second-factor check from
   the user. When a tool says so, tell the user what to do in the workspace. Do not retry around it.
5. **Check before you retry a change.** A repeated call is run only once when it repeats the same
   JSON-RPC id and the same arguments within 30 minutes. Most clients send a new id, so after a timeout
   or an unclear answer, look the record up before you try the change again.

## Privacy

Over MCP, email addresses and phone numbers arrive as placeholders by default. That is on purpose.
An owner or admin can allow full contact details for one key in the key builder. Do not ask the user
to turn it on unless the task truly needs it. Everything you read reaches the user's AI provider, so
read only what the task needs.

## More

- API reference: `https://app.aybiza.com/api/v1/docs`
- AYBIZA: `https://aybiza.com`
