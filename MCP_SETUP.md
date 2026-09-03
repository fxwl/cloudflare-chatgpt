# Cloudflare MCP setup for ChatGPT Web

ChatGPT Web should not consume Cloudflare's MCP servers from `mcp.json` or `.mcp.json` inside this plugin, because imported plugins that declare MCP servers directly are marked **Desktop only**.

Instead, create these MCP endpoints as ChatGPT workspace apps, then reference their existing app IDs from this plugin.

## Recommended Cloudflare MCP apps

| App reference name | MCP endpoint | Authentication |
|---|---|---|
| `cloudflare` | `https://mcp.cloudflare.com/mcp` | OAuth |
| `cloudflare-docs` | `https://docs.mcp.cloudflare.com/mcp` | No auth |
| `cloudflare-bindings` | `https://bindings.mcp.cloudflare.com/mcp` | OAuth |
| `cloudflare-builds` | `https://builds.mcp.cloudflare.com/mcp` | OAuth |
| `cloudflare-observability` | `https://observability.mcp.cloudflare.com/mcp` | OAuth |

Create each endpoint as a custom ChatGPT app in your workspace and complete its authentication/setup.

## Find the app IDs

After each app exists, copy its app ID. Supported app IDs for plugin references begin with one of:

- `asdk_app_`
- `connector_`
- `templated_apps_`

Do not use a `plugin_...` ID.

## Attach the apps to this plugin

Copy `plugins/cloudflare/.app.example.json` to `plugins/cloudflare/.app.json` and replace every placeholder ID with the real app ID.

Then edit:

`plugins/cloudflare/.codex-plugin/plugin.json`

and add this top-level field:

```json
"apps": "./.app.json"
```

The five app references are intentionally optional (`required: false`), so the Cloudflare Skills continue to work even when a particular MCP app is unavailable.

## Important

Do not add any of the following if ChatGPT Web support is required:

- `mcp.json`
- `.mcp.json`
- inline MCP server declarations in the plugin manifest

Those forms cause an imported plugin to be labeled Desktop only.
