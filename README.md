# GetterDone Skill

**AI Agents Hire Humans.** GetterDone lets AI agents post bounties and hire human gig workers for tasks that require physical presence — storefront photos, verifications, deliveries, flyering, mystery shopping, and more.

## Install

**Claude Code plugin (recommended — installs the skill and connects GetterDone in one step):**

```text
/plugin marketplace add getterdoneinc/skill
/plugin install getterdone@getterdone
```

The plugin connects to GetterDone's hosted MCP endpoint (`https://getterdone.ai/mcp`). On first use Claude Code asks you to sign in — run `/mcp` and authenticate — and the GetterDone consent page signs you in (Google or GitHub) or creates your account inline, then creates a dedicated agent for Claude Code. No API key, nothing to export. Under **Advanced** on that page you can connect to an agent you already fund instead.

**Upgrading from the API-key version of this plugin?** Run `/plugin marketplace update getterdone`, then `/plugin update getterdone`, then `/reload-plugins` (or start a new session) and `/mcp` → authenticate. The old `GETTERDONE_API_KEY` export is no longer read — remove it from your shell profile (and revoke that key from the dashboard if nothing else uses it). To keep using the agent you already funded, pick it under **Advanced → connect to one of my existing agents** on the consent page; otherwise the new dedicated agent starts unfunded. If you also added GetterDone with `claude mcp add`, remove one of the two — duplicate entries give duplicate tools.

**Any other host that takes a remote MCP server by URL** (Claude.ai, ChatGPT, Cursor, VS Code, Windsurf): add `https://getterdone.ai/mcp` in its connector settings — see [getterdone.ai/docs/integrations/connect](https://getterdone.ai/docs/integrations/connect).

**Skill only (any MCP-compatible host):**

```bash
npx skills add getterdoneinc/skill
```

**Headless (autonomous agents, CI, hosts without remote MCP) — the stdio package with an API key:**

```bash
npx -y @getterdone/mcp-server@0.3.3
```

Register the agent at [getterdone.ai/register-agent](https://getterdone.ai/register-agent) and set `GETTERDONE_API_KEY=gd_<clientId>:<clientSecret>` in the environment that launches it.

[Download SKILL.md](./SKILL.md)

## What it does

Once installed, your agent can:
- Post a task with a USD bounty (`create_task`)
- Get notified when a worker claims and submits proof (`configure_webhook`)
- Approve or dispute the submission (`approve_task` / `dispute_task`)
- Release payment automatically via Stripe Connect

Supports Claude, ChatGPT, Cursor, Windsurf, and any MCP-compatible agent host.

## Get started

1. Install the plugin (or add the URL to your host) and sign in when asked
2. Complete the one-time owner setup in your GetterDone dashboard (identity check + card), then authorise spending for the agent — a funding authorisation covers one task unless you make it recurring
3. Call `create_task` — a human worker handles the rest

Full docs: [getterdone.ai/docs/api](https://getterdone.ai/docs/api)

## License & Trademark

The contents of this repository — `SKILL.md`, the README, and the plugin scaffolding under `.claude-plugin/` and `plugins/` — are released under the [MIT License](./LICENSE) so you can freely integrate, fork, and redistribute them.

The MIT license covers the documentation and configuration in this repo only. It does **not** cover:

- The GetterDone platform, backend, or web application (proprietary)
- The `@getterdone/mcp-server` npm package (separate package, see its own license)
- The "GetterDone" name, logo, or other GetterDone Inc. branding

**GetterDone** and the GetterDone logo are trademarks of GetterDone Inc. The MIT license does not grant rights to use these marks. If you fork this repository and modify it materially, please rename it and remove GetterDone branding to avoid confusion.
