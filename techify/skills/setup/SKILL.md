---
name: setup
description: Connect and verify the Techify MCP server. Use when a techify tool returns an authentication or authorization error, when the techify tools are missing, when the user wants to switch workspace, or right after installing the plugin.
---

# Techify setup

The plugin registers the remote MCP server `https://api.techify.work/mcp`. There is nothing to install. The user signs in once; the agent stores and refreshes the token.

## 1. Check the state

Call `get-context`.

- Success: you are connected. Go to step 3.
- Authentication error (401): go to step 2.
- Forbidden (403): the member left the workspace or the connection was disconnected. Go to step 2 and sign in again.
- Tool not found: the plugin is not loaded. Ask the user to restart the agent. If it is still missing, repeat the install from `GETTING_STARTED.md` in the plugin repository.

## 2. Sign in

Tell the user what will happen: a browser window opens Techify, they log in with their company account, check the workspace and role shown, and approve.

- **Claude Code:** ask the user to run `/mcp`, choose **techify**, then **Authenticate**. If the browser does not open, the command prints a URL to copy.
- **Codex:** run `codex mcp login techify`. Show the user the URL if needed.
- **Cursor:** ask the user to open the MCP settings, find **techify** and click the login action.
- **No browser (remote sandboxes, CI):** the user creates a personal access token in the workspace under Integrations, AI assistants, and connects with an `Authorization: Bearer` header instead, see `GETTING_STARTED.md`.

The account must be a company account with a company profile. Applicant accounts cannot connect.

## 3. Verify

Call `get-context` again and tell the user in one line: the workspace name, the role, and whether they can publish. Do not print ids or tokens.

## Switching workspace

A connection belongs to the workspace the member works in. To use another workspace, sign in with the account that belongs to it: clear the authentication (Claude Code: `/mcp`, techify, Clear authentication) and sign in again. Disconnecting in Techify under Integrations, AI assistants revokes the connection immediately.
