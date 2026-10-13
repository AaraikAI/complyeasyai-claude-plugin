# Security policy

## Reporting a vulnerability

Please report security issues in this plugin or in the ComplyEasyAI connector
(`https://mcp.complyeasyai.com`) by email to **security@complyeasyai.com**. Do not open a public
GitHub issue for a security report.

Include what you found, the steps to reproduce it and the version of the plugin (from
`plugins/complyeasyai/.claude-plugin/plugin.json`). Do not include real customer data, access
tokens or passwords in your report.

We will acknowledge your report and keep you informed until the issue is resolved.

## Scope

- The contents of this repository: the marketplace definition, the plugin manifest, the MCP server
  declaration, the skills and the agent.
- The hosted connector and its sign-in flow at `mcp.complyeasyai.com`.

Please test only against a ComplyEasyAI workspace you own or are authorized to test. Do not run
denial-of-service tests or automated scans that could affect other customers.

## What this plugin does on your computer

Nothing runs locally: the plugin has no hooks, scripts, executables or local servers. It declares one
remote MCP server, `https://mcp.complyeasyai.com/mcp`. Sign-in tokens are stored by your Claude app,
not by this plugin.
