# Build a desk

1. `list_desks` with `site`. If a desk already does the job, tune it instead of making another.
2. Ask what the desk is for and how it should sound. Draft `persona` (who it is, what it helps
   with, what it must not do) and a one-line `greeting`. Show both and get a yes.
3. `create_desk` with name, tagline, persona, greeting. It returns a draft.
4. Knowledge: `list_sources`. For missing facts (prices, hours, policies), draft the text, show
   it, then `save_source`. Desks answer only from sources; a gap means "I don't know" to visitors.
5. `list_desk_questions` to review intake. Questions are edited in the dashboard.
6. `request_desk_update` with `active: true`. Tell the person to approve it in
   Settings → Agent access.
7. `get_desk_embed` and help paste the tag before `</body>` on the website.

## Failures

- "give at least one field to change": `request_desk_update` needs a field besides `desk_id`.
- "This tool works on one website": pass `site`.
- "No desk …": the id is from another website; call `list_desks` with the right `site`.
