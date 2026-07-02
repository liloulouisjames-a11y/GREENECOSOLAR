# CLAUDE.md — Guidance for Claude Code sessions in this repo

## Keep the context window lean: enable only the connectors you need

Claude Code web/app sessions load the **full tool catalog of every enabled MCP
connector** (tool names, descriptions, and JSON schemas) into the conversation
*before any work starts*. With many connectors enabled, that metadata alone can
fill most of the context window, producing the error:

> "this conversation is too long to continue. Start a new chat, or remove some
> tools to free up space."

This is almost never caused by the code in this repo — it is caused by having
too many integrations turned on for the session.

### Fix / prevention

1. Open the Claude Code web/app UI → **Settings → Connectors** (integrations/MCP).
2. **Disable every connector you do not need for this repository.** For this
   project you typically only need **GitHub**.
3. **Start a new chat.** Connector changes only take effect on a fresh session.

> Starting a new chat *without* disabling connectors will reload them all and
> hit the same limit again — disabling the unused ones is the durable fix.

### Why it can't be fixed by editing a file mid-session

These connectors are **account-level integrations managed by the Claude Code
platform**, not files inside the (ephemeral) session container. There is no
local `mcpServers` config to edit, and changes require a fresh session to apply.

## Recommended connectors for this repo

| Connector | Needed? | Notes |
|-----------|---------|-------|
| GitHub    | Yes     | PRs, issues, CI, branches |
| All others (Adobe, Canva, Figma, Slack, Gmail, QuickBooks, Notion, Stripe, ...) | No | Disable unless a task explicitly needs one |
