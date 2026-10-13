# ComplyEasyAI plugins for Claude

> **Status: pilot.** The ComplyEasyAI connector this plugin uses is in a limited pilot and is not
> generally available yet. The plugin works only for workspaces whose administrator has the AI
> connector turned on; for everyone else, sign-in will not complete. Watch this repository's
> releases for general availability.

This repository is the ComplyEasyAI plugin marketplace for Claude. It holds one plugin,
**ComplyEasyAI** (`plugins/complyeasyai`), which connects Claude to your ComplyEasyAI compliance
workspace through ComplyEasyAI's hosted connector and adds compliance workflows: audit-readiness
briefs, risk and vendor reviews, security questionnaire drafting, auditor-request triage and, in
Claude Code, closing control gaps from your repository.

Read the plugin's own [README](plugins/complyeasyai/README.md) for what it does, what it sends and
fetches, requirements, sign-in and sign-out.

## Install

### Claude Code

```
/plugin marketplace add AaraikAI/complyeasyai-claude-plugin
/plugin install complyeasyai@complyeasyai
```

Then run `/mcp`, choose the ComplyEasyAI server, select **Authenticate** and approve access in
ComplyEasyAI. Try `/complyeasyai:readiness`.

### Claude (web, desktop and Cowork)

Open **Customize**, then **Plugins**, add the marketplace from GitHub
(`AaraikAI/complyeasyai-claude-plugin`), install **ComplyEasyAI**, then open the plugin's
**Connectors** tab and select **Connect**.

You need a ComplyEasyAI workspace whose administrator has turned on the AI connector. Full
documentation: https://www.complyeasyai.com/docs/ai-connectors

## Repository layout

```
.claude-plugin/marketplace.json     marketplace definition (name: complyeasyai)
plugins/complyeasyai/               the plugin
  .claude-plugin/plugin.json        manifest
  .mcp.json                         the one remote MCP server: https://mcp.complyeasyai.com/mcp
  skills/                           six workflow skills and one guidance skill
  agents/audit-prep.md              evidence-gap report agent (Claude Code and Cowork)
  assets/icon.png                   listing icon
tests/plugin.test.mjs               structure and content checks (Node.js built-in test runner)
.github/workflows/validate.yml      runs the checks on every pull request
```

The plugin contains no hooks, scripts, executables or local servers.

## Checks

Before every release, from the repository root:

```
claude plugin validate ./plugins/complyeasyai --strict
claude plugin validate . --strict
node --test tests/plugin.test.mjs
```

`claude plugin validate` needs Claude Code 2.1.281 or later for the MCP checks and the directory
listing fields. The tests need Node.js 22 or later and no packages.

## Releases

Raise `version` in `plugins/complyeasyai/.claude-plugin/plugin.json`, add the entry to
`CHANGELOG.md`, and merge to `main`.

## Security and support

Report vulnerabilities as described in [SECURITY.md](SECURITY.md). For product support, see
https://www.complyeasyai.com/docs/ai-connectors#sec-support

## License

Copyright 2026 AARAIK LLC. Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE).
