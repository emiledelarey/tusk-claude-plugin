---
name: tusk-connect-site
description: Connect a website the user built to Tusk CMS so their client can edit its text and images without touching code. Use when the user asks to "connect this site to Tusk", "make this site client-editable", "let my client edit the copy", "set up Tusk", or to wire a site's build to pull published content from Tusk, in this repo or for a deployed site.
---

# Connect a site to Tusk

Tusk keeps a site's editable words and images and publishes them into the site's own build. Tusk never hosts the site and never holds host credentials: the code stays in this repo, the host stays the developer's, and the build pulls the published content.

The `tusk` MCP server (bundled with this plugin) does the Tusk side. If its tools answer 401, the machine is not paired yet: ask the developer to run, in a terminal,

```bash
npx @tuskcms/mcp login --site <slug> --scopes scan,fields,content,publish,deploy,invite
```

and tap Approve in the browser that opens (omit `--site` the first time, before the site exists). Never ask for or handle a token by hand.

## Steps

1. `whoami`, then `list_sites`. If the site is not there, `create_site` with its name, live `domain` and an https `previewUrl` Tusk can reach.
2. `get_connect_guide` once, to learn the `data-tusk` marking grammar.
3. Decide what the client may edit. Mark those elements in this repo's source with `data-tusk="page.field"` (plus `data-tusk-label` / `data-tusk-kind` where useful). Leave navigation, logos and layout to the developer. Commit and deploy the preview so Tusk can see the marks.
4. `scan_site` with the page URLs, then `get_schema` and check the fields read sensibly. Curate with `save_fields` if needed.
5. `rotate_build_token` writes `TUSK_SITE`, `TUSK_URL` and `TUSK_TOKEN` into `.env` without the token entering this conversation. Set the same `TUSK_TOKEN` on the host by piping it from `.env`, never by printing it.
6. `get_instruction` for this site, and wire the build to run the pull before it builds (for example `npx @tuskcms/sdk pull` or the zero-dependency `tusk-pull.mjs` it names).
7. Create a deploy hook in the developer's host and record it with `set_deploy` (`deployMode: "hook"`), or use `deployMode: "feed"` for a site that fetches content itself.
8. `publish`, then `deploy_status` until it is live. Tell the developer what is live.
9. Only when the developer gives you their client's email: `invite_client`.

## Rules

- Never print, log or commit `TUSK_TOKEN` or the access token. `.env` must be git-ignored (the tool checks and says so).
- Never invite an address the developer did not give you.
- `publish` changes the live website: say what will change before calling it.
