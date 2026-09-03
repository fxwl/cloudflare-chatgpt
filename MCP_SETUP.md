# Cloudflare MCP setup for ChatGPT Web

For ChatGPT Web, keep MCP configuration out of `mcp.json`, `.mcp.json`, and inline server declarations. Imported plugins that directly declare MCP servers are labeled **Desktop only**.

Use one existing ChatGPT workspace app instead.

## Create one Cloudflare workspace app

Create a custom MCP app in the ChatGPT workspace with:

| Setting | Value |
|---|---|
| Name | `Cloudflare` |
| MCP endpoint | `https://mcp.cloudflare.com/mcp` |
| Authentication | OAuth |

Cloudflare's primary MCP is designed as a token-efficient gateway for the entire Cloudflare API. It also includes Cloudflare developer-documentation search, so a separate docs app is not required for the normal ChatGPT workflow.

Cloudflare also publishes specialized MCP servers for bindings, builds, and observability. They can still be added separately if a future workflow specifically needs their specialized tools, but this plugin deliberately uses the primary gateway to keep setup to one app.

## Get the app ID

After creating the app, copy its ChatGPT app ID. Valid plugin app references begin with one of:

- `asdk_app_`
- `connector_`
- `templated_apps_`

Do not use a `plugin_...` ID.

## Attach it to the plugin

1. Copy `plugins/cloudflare/.app.example.json` to `plugins/cloudflare/.app.json`.
2. Replace `asdk_app_REPLACE_CLOUDFLARE` with the real app ID.
3. Add this top-level field to `plugins/cloudflare/.codex-plugin/plugin.json`:

```json
"apps": "./.app.json"
```

The app reference should be marked `required: true` once attached, because this repository is intended to provide both Cloudflare Skills and live Cloudflare MCP access as one plugin.

After committing those two changes, use **Sync now** on the imported marketplace in ChatGPT.

## Why this cannot be fully zero-click from GitHub

GitHub marketplace sync imports plugin content, but it does not create a ChatGPT workspace app, grant access to a provider, or perform Cloudflare OAuth. `.app.json` can only reference an app that already exists in the workspace.

Therefore the minimum one-time setup for ChatGPT Web is:

1. Create one Cloudflare workspace app.
2. Complete Cloudflare OAuth.
3. Put its app ID into this repository once.

After that, plugin and Skills updates can sync automatically from GitHub.
