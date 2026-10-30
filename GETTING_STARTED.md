# Techify getting started guide

This guide is written for an AI coding agent. Follow it step by step in the current session. It installs the Techify plugin for your agent and connects it to the user's Techify company workspace.

The plugin contains no binaries and installs no software. It registers one remote MCP server (`https://api.techify.work/mcp`) and a set of skills.

## 1. Install the plugin

Pick the section for the agent you are running in.

**Claude Code**

```
/plugin marketplace add Uliasti-Agency/techify-agent-plugins
/plugin install techify@techify-plugins
```

If you cannot run slash commands yourself, ask the user to run them, or use the shell equivalents:

```bash
claude plugin marketplace add Uliasti-Agency/techify-agent-plugins
claude plugin install techify@techify-plugins
```

**Codex**

```bash
codex plugin marketplace add Uliasti-Agency/techify-agent-plugins
```

Then open **Plugins** and install **techify**.

**Cursor**

Ask the user to open Settings, Plugins, paste `https://github.com/Uliasti-Agency/techify-agent-plugins` and install **techify**. If the plugin does not appear after installing, clone the repository and follow the `setup` skill as a runbook:

```bash
git clone --depth 1 https://github.com/Uliasti-Agency/techify-agent-plugins.git /tmp/techify-agent-plugins
cat /tmp/techify-agent-plugins/techify/skills/setup/SKILL.md
```

Delete the clone when you are done.

**Any other MCP client**

Add a remote MCP server named `techify` with the URL `https://api.techify.work/mcp` (Streamable HTTP). The client handles OAuth on its own.

## 2. Sign in

The Techify MCP server uses OAuth. The first call fails with an authentication error until the user has signed in once.

- **Claude Code:** run `/mcp`, choose **techify**, choose **Authenticate**. A browser window opens Techify. The user logs in with their company account, checks the workspace and approves. The token is stored by Claude Code and refreshed automatically.
- **Codex:** run `codex mcp login techify` and show the user the URL if the browser does not open.
- **Cursor:** open the MCP settings, find **techify** and click the login action.

The user needs a Techify company account. If they do not have one, send them to https://techify.work/auth/sign-up and ask them to create the company profile first.

Some platforms need a restart before the new skills and the server appear. If the `techify` tools are missing, ask the user to restart the agent.

## 3. Verify

Call the `get-context` tool. It returns the member you act as, the workspace, the role and what it allows, job counts, the price and the payment method. Tell the user in one line which workspace you are connected to and with which role. Do not repeat tokens or ids.

If `get-context` fails with 401, repeat step 2. If it fails with 403, the user is no longer a member of that workspace or the connection was disconnected; sign in again.

## 4. Start working

Read the `techify` skill. It explains what Techify is, which tool to use for which task, and the rules: drafts are free, publishing costs money and needs the user's explicit yes, never claim a job is live unless the tool said so.

## Scripts and CI

For unattended use, the user can create a personal access token in the workspace (Integrations, AI assistants, Create token) and connect without the plugin:

```bash
claude mcp add --transport http techify https://api.techify.work/mcp --header "Authorization: Bearer <token>"
```

Treat the token like a password. Never write it into files that are committed.
