# Techify agent plugins

Hire on [Techify](https://techify.work) from Claude Code, Codex and Cursor.

Techify is the job board for tech jobs in Switzerland. This plugin connects your coding agent to the Techify MCP server and teaches it how to work in your company workspace: turn a job description into a draft, review the drafts that arrive from your ATS, publish jobs after you approve the price, and read the applications. The agent acts as you, in one workspace, with your role. Drafts are free and private; nothing is published or paid without your confirmation.

## Setup

**If you are an AI agent:** read [GETTING_STARTED.md](GETTING_STARTED.md) and follow it as a runbook. If you cannot fetch it from this page, run:

```bash
curl -fsSL https://raw.githubusercontent.com/Uliasti-Agency/techify-agent-plugins/main/GETTING_STARTED.md
```

**If you are a person:** paste this into your coding agent:

> Set up the Techify plugin by following the steps in https://github.com/Uliasti-Agency/techify-agent-plugins

Or install by hand:

| Agent | Steps |
| --- | --- |
| Claude Code | `/plugin marketplace add Uliasti-Agency/techify-agent-plugins` then `/plugin install techify@techify-plugins`, then `/mcp` to sign in |
| Codex | `codex plugin marketplace add Uliasti-Agency/techify-agent-plugins`, install **techify** under Plugins, then `codex mcp login techify` |
| Cursor | Settings, Plugins, paste `https://github.com/Uliasti-Agency/techify-agent-plugins`, install **techify**, then sign in when the MCP server asks |

Signing in opens Techify in your browser. You log in with your Techify company account, check the workspace the agent will work in, and approve. You can disconnect at any time in your workspace under Integrations, AI assistants.

Claude.ai, Claude Desktop, ChatGPT and VS Code connect without the plugin: add `https://api.techify.work/mcp` as a custom connector. See https://techify.work/integrations/ai.

## What is in the plugin

- `techify/.mcp.json` connects the agent to the Techify MCP server at `https://api.techify.work/mcp` (Streamable HTTP, OAuth 2.1).
- `techify/skills/` teaches the agent how to use it well. Start with the `techify` skill; it routes to the others.

| Skill | Use it for |
| --- | --- |
| `techify` | Start here. What Techify is, which tool does what, the rules. |
| `setup` | Check the connection, sign in, verify. |
| `draft-job` | Turn a job description, a link or notes into a Techify draft. |
| `review-drafts` | Go through drafts from your ATS, feed or API; keep or discard. |
| `publish-jobs` | Publish drafts after the user approves the price. |
| `applications` | Read and summarise the applications to your jobs. |
| `hiring-report` | Live jobs, expiring jobs, applications and open charges at a glance. |
| `feedback` | Where to report a problem. |

## Pricing

The MCP server is included in every Techify workspace. Drafts are free. Publishing a job costs CHF 95 for 60 days, paid by card or, for approved companies, on invoice.

## Support

Questions and bug reports: hello@techify.work or [open an issue](https://github.com/Uliasti-Agency/techify-agent-plugins/issues).

Documentation: https://techify.work/integrations/ai.
