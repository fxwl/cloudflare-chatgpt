---
name: cloudflare
description: Cloudflare platform guidance for Workers, Pages, D1, R2, KV, Durable Objects, Agents SDK, Wrangler, Email Service, Cloudflare One, security, networking, builds, and observability. Use for Cloudflare development, deployment, configuration, troubleshooting, and account-operation workflows. Prefer current Cloudflare documentation and connected Cloudflare workspace apps over stale model knowledge.
---

# Cloudflare

Use this skill for Cloudflare platform work.

1. Prefer current Cloudflare documentation before giving exact API shapes, limits, pricing, compatibility flags, or CLI syntax.
2. If a Cloudflare workspace app is connected, use it for live account state, builds, bindings, logs, or other supported account operations instead of asking the user to copy data manually.
3. For code changes, inspect the project configuration first (`wrangler.jsonc`, `wrangler.toml`, package metadata, framework config) and preserve the project's existing conventions.
4. For deployments, verify bindings and resource identifiers before deploying. Do not invent account IDs, zone IDs, database IDs, bucket names, or secrets.
5. For Email Service, distinguish Email Routing (inbound/forwarding) from Email Sending (outbound transactional mail), and verify domain onboarding/authentication before suggesting sending configuration.
6. When a task spans several Cloudflare products, explain the architecture briefly, then execute or propose the smallest viable set of resources.

This repository automatically synchronizes Cloudflare's full official Skills set from `cloudflare/skills`. If the synchronized product-specific skill is available, prefer that more specific skill.
