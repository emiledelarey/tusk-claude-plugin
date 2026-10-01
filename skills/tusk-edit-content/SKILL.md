---
name: tusk-edit-content
description: Change the text on a Tusk-connected website and publish it. Use when the user asks to update, rewrite or fix copy on a site managed in Tusk CMS ("change the hero headline on suntex", "fix the typo on the about page", "update the opening hours") rather than editing the code.
---

# Edit a Tusk site's text

1. `list_sites` to find the site's slug, then `get_site` to find the page key.
2. `get_page` to see each editable field's id and current text.
3. `update_text` for each field to change. This saves a draft; the live site is unchanged.
4. Show the developer the before and after, then `publish` (only the pages you changed, via `pages`).
5. `deploy_status` until the host reports it is live.

Text and multi-line text fields only. Photos, files and lists are edited in the Tusk editor at https://tuskcms.com. If a field is locked, say so; do not work around it by editing the code.
