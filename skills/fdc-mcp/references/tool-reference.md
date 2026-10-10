# Tool reference

The live `tools/list` is authoritative. Scope in brackets.

## Websites and numbers
- `list_sites` [read] — the websites this connection may name; ids for `site`.
- `get_site` [read] — one website's settings.
- `get_analytics_overview` [read] — chats, bookings, funnel, CSAT, escalations for a window.

## Desks
- `list_desks`, `get_desk`, `list_desk_questions` [read] — configuration and intake questions.
- `get_desk_embed` [read] — the `<script>` tag for the website.
- `create_desk` [write] — a draft desk, not live.
- `request_desk_update` [publish] — asks for a change to name, tagline, persona, greeting,
  `widget_config` or `active`. Pending until the owner approves.

## Inbox
- `get_inbox_counts` [read] — conversations handed off and waiting for a person.
- `list_conversations`, `get_conversation` [read] — filters: `desk_id`, `status`, `visitor_id`, `q`.
- `close_conversation`, `reopen_conversation` [write] — status only; nothing is sent.
- `list_visitors`, `get_visitor` [read].

## Bookings and availability
- `list_bookings` [read].
- `list_schedules`, `get_schedule` [read] — account-wide; `site` does not apply.

## Knowledge
- `list_sources` [read] — the pages desks answer from.
- `save_source` [write] — creates, or replaces the text of the source with the same title.
- `list_skills` [read] — account-wide.

## Not on the server
Replying to visitors, confirming or cancelling bookings, erasing visitors, any delete, editing
intake questions, keys, billing, integrations, account settings.
