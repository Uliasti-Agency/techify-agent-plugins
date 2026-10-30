# Techify getting started guide

This guide is written for an AI coding agent. Follow it step by step in the current session. It installs the Techify plugin for your agent and connects it to the user's Techify account: a company workspace or a candidate account.

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

- **Claude Code:** run `/mcp`, choose **techify**, choose **Authenticate**. A browser window opens Techify. The user logs in with their company or candidate account, checks what you will be able to do and approves. The token is stored by Claude Code and refreshed automatically.
- **Codex:** run `codex mcp login techify` and show the user the URL if the browser does not open.
- **Cursor:** open the MCP settings, find **techify** and click the login action.

The user needs a Techify account. Companies sign up at https://techify.work/auth/sign-up/company and create the company profile first; candidates sign up at https://techify.work/auth/sign-up/applicant.

Some platforms need a restart before the new skills and the server appear. If the `techify` tools are missing, ask the user to restart the agent.

## 3. Verify

If the server offers `get-context`, the user is a company: call it. It returns the member you act as, the workspace, the role and what it allows, job counts, the price and the payment method. Tell the user in one line which workspace you are connected to and with which role. If it offers `get-profile` instead, the user is a candidate: call it and tell them in one line whether their profile is ready to apply. Do not repeat tokens or ids.

If the call fails with 401, repeat step 2. If it fails with 403, the user is no longer a member of that workspace (or no longer has a candidate account) or the connection was disconnected; sign in again.

## 4. Start working

Read the `techify` skill. It explains what Techify is, which tool to use for which task, and the rules: drafts are free, publishing costs money and needs the user's explicit yes, never claim a job is live unless the tool said so.

## Scripts and CI

For unattended use, the user can create a personal access token (companies: Workspace, Integrations, AI assistants; candidates: My Techify, AI assistants; then Create token) and connect without the plugin:

```bash
claude mcp add --transport http techify https://api.techify.work/mcp --header "Authorization: Bearer <token>"
```

Treat the token like a password. Never write it into files that are committed.
