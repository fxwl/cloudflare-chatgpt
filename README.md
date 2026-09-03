# Cloudflare for ChatGPT

ChatGPT Web-compatible packaging of Cloudflare's official Skills with one optional Cloudflare MCP workspace app for live account access.

## Architecture

This repository intentionally does **not** declare `mcp.json`, `.mcp.json`, or inline MCP servers, because ChatGPT marks imported plugins that directly declare MCP servers as **Desktop only**.

Instead it uses:

- Cloudflare's official Skills, synced from `cloudflare/skills`
- a native ChatGPT/Codex plugin manifest
- one optional `.app.json` reference to an existing ChatGPT workspace app
- that app connects directly to Cloudflare's primary MCP endpoint: `https://mcp.cloudflare.com/mcp`

Cloudflare's primary MCP is a Code Mode gateway for the full Cloudflare API and includes developer-documentation search. It exposes a compact `docs`, `search`, and `execute` tool surface rather than thousands of individual API tools.

## Import into ChatGPT

In your ChatGPT workspace:

1. Open **Workspace settings -> Plugins -> Add -> Import marketplace**.
2. Source: `https://github.com/fxwl/cloudflare-chatgpt`
3. Path: leave empty.
4. Branch: `main` or leave empty to use the default branch.
5. Import and configure the Cloudflare plugin installation policy.

The Skills portion works without MCP setup.

## One-time MCP setup

For live Cloudflare account access, create **one** custom ChatGPT workspace app:

- Name: `Cloudflare`
- MCP URL: `https://mcp.cloudflare.com/mcp`
- Authentication: OAuth

After the app exists, copy its app ID (`asdk_app_...`) and follow [`MCP_SETUP.md`](MCP_SETUP.md). The repository can then reference that single app, so the plugin contains both the official Skills and live Cloudflare access while remaining usable on ChatGPT Web.

The GitHub marketplace import itself cannot create or authorize a workspace app; ChatGPT requires that app to exist first. Cloudflare OAuth is also intentionally user-authorized.

## Upstream Skills sync

`.github/workflows/sync-cloudflare-skills.yml` synchronizes the official `skills/` directory, Cloudflare logo, and license from `https://github.com/cloudflare/skills` every day and can also run manually.

The upstream commit used for the last successful sync is recorded in `plugins/cloudflare/UPSTREAM_COMMIT`.

## License

Cloudflare's synced materials remain subject to the upstream Apache-2.0 license. See `plugins/cloudflare/LICENSE` after the first successful sync.
