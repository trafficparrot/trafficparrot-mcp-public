# Traffic Parrot MCP server

A public MCP server run by Traffic Parrot, so that your AI coding agent can request a Traffic Parrot trial, read the product documentation and send us feedback. Traffic Parrot is a service virtualization tool: it simulates the APIs and messaging systems your software depends on, for testing.

The server is hosted by Traffic Parrot at `https://mcp.trafficparrot.com/` (remote MCP over streamable HTTP; registry name `com.trafficparrot/public`). This repository holds only its listing metadata, no server code. Issues and feature requests are welcome through the `submit_feature_request` tool or support@trafficparrot.com.

Also listed on [Glama](https://glama.ai/mcp/connectors/com.trafficparrot/public) and [Smithery](https://smithery.ai/servers/trafficparrot/public).

## Add it to your agent

### Claude Code

```
claude mcp add --transport http trafficparrot https://mcp.trafficparrot.com/
```

### Cursor

Add this to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "trafficparrot": {
      "url": "https://mcp.trafficparrot.com/"
    }
  }
}
```

### Any other client

Any client that supports remote MCP over streamable HTTP can use it: add a server with the URL `https://mcp.trafficparrot.com/`. The shapes for Cline and VS Code are in [llms-install.md](llms-install.md).

## No API key

There is nothing to sign up for and no key to configure. Requests are rate limited.

## The tools

- `request_trial`: asks Traffic Parrot for a trial on your behalf. You give your business email; the trial link is sent to that inbox, never to the agent.
- `get_trial_status`: checks the state of a trial request: waiting for approval, being prepared, ready, or unavailable. The reply is the state only; the trial link still goes to your inbox, never to the agent.
- `delete_trial_request`: withdraws a trial request and erases the details sent with it.
- `get_trial_onboarding`: explains how to get Traffic Parrot running from the trial download. It covers the ports it uses, starting and stopping it on each operating system, where the licence goes, and a first mock for each protocol.
- `get_documentation`: the Traffic Parrot documentation index, in a form written for agents.
- `submit_feature_request`: sends a feature request or feedback to the Traffic Parrot team.

A person at Traffic Parrot approves each trial request during UK working hours, so a trial is not instant. How the trial route works: https://trafficparrot.com/ai/agent-trial.html

## Which server this is

This is the public server run by Traffic Parrot, the company, for finding out about and trying the product. It is not the MCP server built into a Traffic Parrot installation, which runs alongside your own licensed instance.

## Privacy

`request_trial` sends a real person's business email, and any name, company or phone number given with it, to Traffic Parrot. Read the [privacy notice](https://trial.trafficparrot.com/privacy) before your agent calls it.

[trafficparrot.com](https://trafficparrot.com)
