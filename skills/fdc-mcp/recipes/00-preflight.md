# Preflight — always first

1. Call `tools/list`. Note which scopes the connection has from what is listed: no
   `create_desk` means no `write`; no `request_desk_update` means no `publish`.
2. Call `list_sites`. If there is more than one, ask which website, or name the one you pick.
   Pass its id as `site` on every later website tool (not on the account-wide `list_sites`,
   `list_schedules`, `get_schedule`, `list_skills`).
3. Call `get_analytics_overview` with `site` for the numbers.
   - Zero chats usually means the widget is not on the website yet, not that nobody visits.
     Offer `get_desk_embed` and help install it.
   - A desk with `active: false` is a draft; visitors cannot chat with it.

## What a failure means

- **401**: the key is missing, mistyped or revoked. Keys start with `fdck_` and are created in
  Settings → Agent access. A connector token expired: reconnect from the client.
- **403 on connect**: the `x-fdc-site` header names a website not on this account.
- **429**: too many calls this minute; wait for `Retry-After` seconds.
- **"lacks the write/publish scope"**: the key was created without it. The owner makes a new key.
- **"This connection is limited to one website"**: a connector approved for one site; drop `site`.
- **"may not have been saved"**: the outcome is unknown. Read the item again before retrying.
