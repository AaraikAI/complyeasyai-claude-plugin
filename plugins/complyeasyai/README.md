# ComplyEasyAI plugin for Claude

Work with your ComplyEasyAI compliance workspace from Claude. The plugin connects Claude to your
workspace through ComplyEasyAI's hosted connector and adds ready-made compliance workflows:
audit-readiness briefs, weekly risk reviews, vendor reviews, security questionnaire drafting,
auditor-request triage and, in Claude Code, closing control gaps from your code repository. Answers
link back to the records in ComplyEasyAI.

Works with Claude Code, Claude (web and desktop) and Cowork.

## Requirements

- A ComplyEasyAI workspace whose administrator has turned on the AI connector (Settings, AI
  connector). Every ComplyEasyAI plan includes the AI connector with a monthly allowance of calls.
- Your own ComplyEasyAI account. Claude sees only what your role can see in ComplyEasyAI.
- Every successful tool call counts toward your workspace's monthly allowance, which the whole
  workspace shares. Usage above the allowance is available only if your administrator opts in, and
  only up to a monthly limit your administrator controls. Your workspace administrator can see
  usage under Settings, AI connector.
- We recommend connecting from the Claude account your organization provides rather than a personal
  one.

## What is included

| Command | What it does |
|---|---|
| `/complyeasyai:readiness [framework]` | Audit-readiness brief: readiness, weakest controls with owners, evidence gaps and next steps |
| `/complyeasyai:risk-review` | Weekly risk review: changes worth discussing, risks without owners or mitigation, overdue reviews |
| `/complyeasyai:vendor-review <vendor>` | Vendor review before renewal: risk level, review dates, related risks and renewal questions |
| `/complyeasyai:questionnaire <questionnaire>` | Draft answers for a security questionnaire, citing your policies and controls, with unsupported items flagged |
| `/complyeasyai:auditor-requests` | Overdue and due-soon auditor requests, with the evidence already on record and the gaps |
| `/complyeasyai:control-evidence [framework]` | Claude Code: controls that your repository can address, with proposed changes per control |

The plugin also includes a guidance skill, `complyeasyai-guide`, that Claude loads on its own to use
the ComplyEasyAI tools carefully, and an `audit-prep` agent (Claude Code and Cowork) that compiles an
evidence-gap report for one framework in its own context window. You can also ask Claude about your
workspace in your own words without a command.

## What the plugin runs, sends and fetches

- **One remote connector.** The plugin declares a single MCP server,
  `https://mcp.complyeasyai.com/mcp`, operated by ComplyEasyAI. It connects to nothing else.
- **Nothing runs on your computer.** No hooks, scripts, executables or local servers. The skills and
  the agent are written instructions for Claude.
- **What ComplyEasyAI receives:** only the tool requests Claude sends while you use it, such as a
  search term, a record id or a filter, under your own ComplyEasyAI permissions. ComplyEasyAI does
  not receive your conversation. Arguments to read tools are not stored. ComplyEasyAI keeps
  connection metadata (tool names, times, the app's identity and a shortened IP address) to provide
  the service.
- **What Claude receives:** the records the tools return, such as frameworks, controls, evidence
  file names and dates (never the files themselves), risks, policies, vendors, auditor requests and
  questionnaires.
- **Changes are off unless your administrator allows them.** Where a workspace allows changes
  (adding or updating risks, updating a control's status, creating issues or comments, drafting
  policies), the change tools are marked as making changes so that Claude can ask before running
  them, and the plugin's skills tell Claude to state each change and wait for your yes. Whether
  Claude actually asks depends on your Claude settings and mode: some modes, such as Research, run
  tools without asking, and on Team and Enterprise plans an Owner sets tool permissions. Every change
  is recorded in ComplyEasyAI's audit trail under your name, and policies are only ever created as
  drafts.
- **Local files (Claude Code only).** The `control-evidence` command asks Claude Code to read files
  in your current repository, with Claude Code's usual permissions, to propose changes. File
  contents are not sent to ComplyEasyAI. The skill tells Claude to apply a change only after you
  agree to it and never to commit or push; your Claude Code permission settings decide whether file
  edits prompt you.

## Install

### Claude Code

```
/plugin marketplace add AaraikAI/complyeasyai-claude-plugin
/plugin install complyeasyai@complyeasyai
```

Once the plugin is listed in Anthropic's plugin directory, you can also install it from
`/plugin directory`, or install it on claude.ai and let it sync to Claude Code.

### Claude (web, desktop and Cowork)

1. Open **Customize**, then **Plugins**, and add the marketplace from GitHub:
   `AaraikAI/complyeasyai-claude-plugin`.
2. Install **ComplyEasyAI**.
3. Open the plugin's **Connectors** tab and select **Connect**.

On Claude Team and Enterprise plans, an Owner decides which plugins and connectors members can use.

## Sign in and sign out

- **Claude Code:** run `/mcp`, choose the ComplyEasyAI server (`plugin:complyeasyai:complyeasyai`) and
  select **Authenticate**. Your browser opens ComplyEasyAI: sign in as usual (password, magic link,
  single sign-on or two-factor, as your account requires), check the app shown on the consent screen
  and approve. To sign out, choose **Clear authentication** in `/mcp`.
- **Claude (web, desktop and Cowork):** select **Connect** on the plugin's Connectors tab, sign in to
  ComplyEasyAI and approve. Disconnect from the same tab.
- **Revoke from ComplyEasyAI at any time:** Settings, My connections. Workspace administrators can
  revoke any connection in the workspace.

If you add ComplyEasyAI both through this plugin and directly as a connector, Claude Code keeps one
of them, so the tools are not duplicated. We recommend one install path per computer.

## Documentation, privacy and support

- Documentation: https://www.complyeasyai.com/docs/ai-connectors
- Privacy policy: https://www.complyeasyai.com/legal/privacy
- Terms of service: https://www.complyeasyai.com/legal/terms
- Support: https://www.complyeasyai.com/docs/ai-connectors#sec-support

ComplyEasyAI is a product of AARAIK LLC. This plugin is licensed under the Apache License 2.0 (see
`LICENSE`).
