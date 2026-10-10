# Triage the inbox

1. `get_inbox_counts`. Handed-off conversations come first: a visitor is waiting for a person.
2. `list_conversations` with `status: "handed_off"`, then `get_conversation` on each. Summarise
   what the visitor needs and draft a reply for the person to send from the dashboard.
3. For a period summary, `list_conversations` (all pages) and group by what visitors asked.
   Questions the desk could not answer point to a missing knowledge source (see fdc-desks).
4. `list_bookings` for upcoming appointments; tie each to its conversation when it matters.
5. Offer to `close_conversation` the ones that are resolved; list them and get a yes first.

## Failures

- "No conversation …": the id belongs to another website; pass the right `site`.
- An empty list with a `site` chosen: check `list_sites` to be sure it is the right website.
