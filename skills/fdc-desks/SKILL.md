---
name: fdc-desks
description: Build, review and tune FrontDeskChat desks (AI front desks on a website) through MCP. Use for creating a desk, reviewing its persona and greeting, checking intake questions, adding knowledge sources, getting the embed code, or putting a desk live. Do not use for connection setup (fdc-mcp) or reading conversations and bookings (fdc-inbox). Trigger on phrases like "create a front desk", "change my desk's greeting", "add this page to what the desk knows", "get the embed code", or "put the desk live".
metadata:
  mcp_tools: 22
---

# FrontDeskChat — desks

A desk is an AI front desk on one website. It greets visitors, asks its intake questions,
answers only from the website's knowledge sources, and can book appointments.

## Ground rules

1. Run [fdc-mcp preflight](../fdc-mcp/recipes/00-preflight.md) first and pass `site`.
2. **Read before you write.** `get_desk` first; `request_desk_update` replaces each field it is
   given, and `widget_config` is replaced whole. Send the full `widget_config` you want.
3. **Drafts first.** `create_desk` makes an inactive draft. Going live is
   `request_desk_update` with `active: true`, which the owner approves.
4. **Nothing you request is live** until approved. Say "requested", never "updated".
5. **Knowledge is live at once.** `save_source` changes live answers immediately and replaces the
   text of a source with the same title. Show the text to the person before saving.

Recipe: [build-a-desk](recipes/build-a-desk.md). Tool details:
[tool-reference](../fdc-mcp/references/tool-reference.md).
