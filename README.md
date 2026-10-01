# Tusk for Claude Code

Let your clients edit the sites you build. This plugin adds the Tusk CMS MCP server and two skills to Claude Code:

- **tusk-connect-site**: connect a site in this repo to Tusk (mark editable parts, scan, wire the build, set the deploy hook, publish, invite the client).
- **tusk-edit-content**: change a connected site's text and publish it.

## Install

```
/plugin marketplace add emiledelarey/tusk-claude-plugin
/plugin install tusk@tuskcms
```

Then pair this machine once (one Approve tap in your browser):

```bash
npx @tuskcms/mcp login
```

## What it can and cannot do

Tusk never hosts your site and never holds your host's credentials. The access token is limited to the sites and actions you approve, expires by itself, and can be revoked in Tusk under Studio settings > Connected tools & devices.

Using claude.ai or the Claude desktop app instead? Add the Tusk connector from the Connectors directory, or add `https://tuskcms.com/mcp` as a custom connector.

Docs: https://tuskcms.com/docs/ai-assistants · Support: hello@tuskcms.com · Privacy: https://tuskcms.com/privacy
