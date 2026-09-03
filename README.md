# Cloudflare for ChatGPT

ChatGPT Web-compatible packaging of Cloudflare's official Skills, with optional references to Cloudflare MCP apps created in your ChatGPT workspace.

## Why this repository exists

Cloudflare's upstream `cloudflare/skills` plugin declares MCP servers directly. ChatGPT marks imported plugins that declare `mcp.json`, `.mcp.json`, or inline MCP servers as **Desktop only**. This repository intentionally does **not** include direct MCP server declarations.

Instead it uses:

- Cloudflare's official Skills, synced from `cloudflare/skills`
- a native ChatGPT/Codex plugin manifest
- an optional `.app.json` reference to existing ChatGPT workspace apps for MCP access

This keeps the plugin usable in ChatGPT Web.

## Import into ChatGPT

In your ChatGPT workspace:

1. Open **Workspace settings -> Plugins -> Add -> Import marketplace**.
2. Source: `https://github.com/fxwl/cloudflare-chatgpt`
3. Path: leave empty.
4. Branch: `main` (or leave empty to use the default branch).
5. Import, then set the Cloudflare plugin installation policy as desired.

The Skills portion works without MCP setup.

## MCP setup

For live Cloudflare account/API/build/log access, create the five custom MCP apps listed in [`MCP_SETUP.md`](MCP_SETUP.md). After you have their ChatGPT app IDs, populate `plugins/cloudflare/.app.json` from the provided example and add `"apps": "./.app.json"` to the native plugin manifest.

Do **not** add `mcp.json`, `.mcp.json`, or inline MCP server declarations to this repository if ChatGPT Web support is required.

## Upstream sync

`.github/workflows/sync-cloudflare-skills.yml` syncs the official `skills/` directory, Cloudflare logo, and license from:

`https://github.com/cloudflare/skills`

The workflow runs daily and can also be run manually. The upstream commit used for the last sync is recorded in `plugins/cloudflare/UPSTREAM_COMMIT`.

## License

Cloudflare's synced materials remain subject to the upstream Apache-2.0 license. See `plugins/cloudflare/LICENSE` after the first sync.
