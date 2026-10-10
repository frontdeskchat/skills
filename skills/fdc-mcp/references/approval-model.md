# Approval model

| Risk | Scope | Examples | Who decides |
|---|---|---|---|
| Read | `read` | every `list_*` / `get_*` | runs at once |
| Visible, undoable write | `write` | `create_desk`, `save_source`, `close_conversation` | runs at once; owner can undo in the dashboard |
| Reaches visitors | `publish` | `request_desk_update` | **owner approves** in Settings → Agent access |

## What "pending" means

`request_desk_update` stores the desk before and after and returns `status: "pending"`. Visitors
see nothing new until a signed-in owner approves. An API key or connector cannot approve, so do
not ask it to. Asking again for the same desk updates the one pending request.

Say: "I've requested the change; it goes live when you approve it in Settings → Agent access."
Never say it is live.

## Server-enforced versus conversational

Enforced by the server: scopes, the website lock, approval of desk changes, withheld tools.
Only conversational: asking the person before `save_source` or `close_conversation`. That is
good practice, not a guard; the server runs those writes when called.

`save_source` changes what live desks answer from, immediately. Confirm the text first.
