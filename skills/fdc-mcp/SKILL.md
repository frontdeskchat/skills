---
name: fdc-mcp
description: Connect an AI agent to FrontDeskChat's remote MCP server and read its tool surface. Use for FrontDeskChat API keys, the MCP URL, OAuth connectors, choosing a website (site), scopes, and MCP errors. Do not use for building desks (fdc-desks) or working the inbox (fdc-inbox). Trigger on phrases like "connect Claude to FrontDeskChat", "frontdeskchat MCP URL", "fdc API key", "which FrontDeskChat tools are there", or "scope to one website".
metadata:
  mcp_tools: 22
  mcp_tools_read: 17
  mcp_tools_write: 4
  mcp_tools_publish: 1
---

# FrontDeskChat — MCP connection

FrontDeskChat puts AI front desks on a business's website: a desk chats with visitors, answers
from the site's knowledge sources and books appointments. An account can hold several websites
(sites); every desk, conversation, visitor and booking belongs to one.

## Ground rules

1. **The live server wins.** Call `tools/list` first. If it disagrees with this file, trust it
   and say this file is out of date.
2. **Pick a website before reading.** Call `list_sites`, name the site back to the person, then
   pass its id as the `site` argument on every website tool. Without `site`, tools read across
   all websites, which looks exactly like one website's data. `list_sites`, `list_schedules`,
   `get_schedule` and `list_skills` are account-wide and take no `site`.
3. **Scopes decide what you see.** A credential carries `read`, `write` and/or `publish`. A new
   key is read-only. Tools above the scope are not listed and are refused if called.
4. **Withheld on purpose.** There is no tool to reply to a visitor, confirm or cancel a booking
   (both reach a real person), erase a visitor or delete anything (irreversible), manage keys,
   billing or integrations. Do not promise these; point the person to the dashboard.
5. **Requests are not changes.** `request_desk_update` returns `pending`. Nothing changes for
   visitors until the owner approves it in Settings → Agent access. Never say it is live.

## Connecting

- URL: `https://api.frontdeskchat.com/mcp` (Streamable HTTP).
- Claude.ai, ChatGPT: add the URL as a custom connector; sign in and approve. The consent screen
  may narrow scopes and lock the connection to one website; then `site` is refused. Disconnect
  it any time in Settings → Agent access → Connected apps.
- Claude Code, Codex, VS Code, Cursor: add the URL and sign in (OAuth); setup lines are in
  Settings → Agent access. Scripts: `Authorization: Bearer fdck_...`, a key created there.
  Optional header `x-fdc-site: <site id>` sets a default website.

Read [00-preflight](recipes/00-preflight.md) before any task,
[tool-reference](references/tool-reference.md) for the tools by job,
[approval-model](references/approval-model.md) for what needs a person, and
[known-gaps](references/known-gaps.md) before offering anything not listed.
