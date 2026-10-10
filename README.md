# FrontDeskChat skills

Agent skills for running [FrontDeskChat](https://frontdeskchat.com) — AI front desks on your
website, the conversations they have, and the bookings they make — over MCP.

- **`fdc-mcp`** — connect an agent safely and read the tool surface.
- **`fdc-desks`** — build and tune desks, their knowledge and embed code.
- **`fdc-inbox`** — triage conversations, visitors and bookings.

## Install

```bash
npx skills add frontdeskchat/skills --global --agent claude-code
npx skills add frontdeskchat/skills --global --agent claude-code --skill fdc-inbox
npx skills add frontdeskchat/skills#v0.1.0 --global --agent claude-code   # pin a release
```

Always pass `--agent`: without it a non-interactive run installs into every agent it knows.

## Connect

The MCP server is `https://api.frontdeskchat.com/mcp` (Streamable HTTP).

Every client signs in with OAuth. The same steps are in Settings → Agent access.

- **Claude**: Settings → Connectors → Add custom connector, paste the URL, sign in.
- **ChatGPT**: Settings → Apps → Create app (developer mode), paste the URL, sign in.
- **Claude Code**: `claude mcp add frontdeskchat https://api.frontdeskchat.com/mcp --scope user --transport http`, then `/mcp`.
- **Codex**: `codex mcp add frontdeskchat --url https://api.frontdeskchat.com/mcp`.
- **VS Code** (`.vscode/mcp.json`): `{"servers": {"frontdeskchat": {"type": "http", "url": "https://api.frontdeskchat.com/mcp"}}}`
- **Cursor** (`~/.cursor/mcp.json`): `{"mcpServers": {"frontdeskchat": {"type": "http", "url": "https://api.frontdeskchat.com/mcp"}}}`

Scripts and CI can send `Authorization: Bearer fdck_...` with a key from Settings → Agent access.

## Use

Ask in your own words; the skill loads on phrases like "any chats waiting for me" or
"change my desk's greeting". In Codex, name it: `Use $fdc-inbox to …`.

## Verify

Run `/mcp` in Claude Code (or your client's equivalent) and check that `list_sites` is listed.
The live `tools/list` is the source of truth for what the server offers.
