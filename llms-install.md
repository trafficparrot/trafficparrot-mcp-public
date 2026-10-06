# Installing the Traffic Parrot MCP server

Instructions for an AI agent adding this server to the MCP client it is running in.

This is a remote MCP server over streamable HTTP at `https://mcp.trafficparrot.com/`. There is nothing to install, no API key and no account: add the URL to your client's MCP configuration and connect. The server name below is `trafficparrot`; any name works.

## Claude Code

Run:

```
claude mcp add --transport http trafficparrot https://mcp.trafficparrot.com/
```

## Cursor

Edit `~/.cursor/mcp.json` (global) or `.cursor/mcp.json` in the project (project only). Add the entry under `mcpServers`; no `type` field is needed, Cursor detects the transport from the URL:

```json
{
  "mcpServers": {
    "trafficparrot": {
      "url": "https://mcp.trafficparrot.com/"
    }
  }
}
```

## Cline

Edit the file that "Configure MCP Servers" opens in the MCP Servers panel (`cline_mcp_settings.json`; the Cline CLI reads `~/.cline/mcp.json` instead). Add the entry under `mcpServers`:

```json
{
  "mcpServers": {
    "trafficparrot": {
      "type": "streamableHttp",
      "url": "https://mcp.trafficparrot.com/",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

`type` must be exactly `streamableHttp`. Leaving it out, or writing `streamable-http`, makes Cline fall back to the legacy SSE transport, which this server answers with 405.

## VS Code

Edit `.vscode/mcp.json` in the workspace, or the user-profile `mcp.json` (the command "MCP: Open User Configuration"). The top-level key is `servers`, not `mcpServers`, and `type` is required:

```json
{
  "servers": {
    "trafficparrot": {
      "type": "http",
      "url": "https://mcp.trafficparrot.com/"
    }
  }
}
```

Without `type`, VS Code treats the entry as a local command and fails to start it.

## Any other client

Add a remote server of transport streamable HTTP with the URL `https://mcp.trafficparrot.com/`. No headers are needed.

## After connecting

Call `get_documentation` first. It returns the Traffic Parrot documentation index written for agents: what Traffic Parrot does, the protocols it simulates, and a link to every reference page. The other tools:

- `get_trial_onboarding`: how to get a downloaded trial running (ports, start and stop per operating system, where the licence goes, a first mock per protocol). Read it once your user has the download.
- `request_trial`: asks Traffic Parrot for a trial on behalf of your user. Call it only when your user has asked for a trial: show them the evaluation agreement the tool description links to, ask for their work email, and do not invent an address. A person at Traffic Parrot approves each request during UK working hours, so it is not instant. The trial link goes only to your user's email; the tool returns a reference id and never a link, so relay the email steps to your user instead of waiting for a download.
- `get_trial_status`: the state of a request, by its reference id.
- `delete_trial_request`: withdraws a request and erases the personal data sent with it.
- `submit_feature_request`: sends the Traffic Parrot team a feature request or feedback.

Once Traffic Parrot is installed and running, it serves its own MCP server on your user's machine for driving that instance; this public server does not control an installation.
