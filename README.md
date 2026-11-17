# RiseMore MCP Server

Connect Codex, Cursor, Claude Code, or another MCP client to your saved RiseMore marketing data. Read products, research, keywords, channels, and social posts, and publish a social post after it has been approved and scheduled in RiseMore.

[RiseMore](https://www.risemore.app/) is your AI marketer, with four agents for SEO, GEO, Reddit, and Social. The [Console](https://www.risemore.app/console) is where you set up products, run the agents, generate and edit content, approve work, and publish SEO/GEO articles. This repository provides connection instructions for the hosted MCP server.

## Connect

- **Server name:** `risemore`
- **Transport:** Streamable HTTP
- **Endpoint:** `https://www.risemore.app/mcp`
- **Authentication:** OAuth with your RiseMore account

No npm package or local server process is required. Sign in through your client's browser authorization flow; you do not need to create an API key or paste a token into your configuration.

One connection covers the products owned by the account you authorize. The eight read tools are available on the Free plan. Publishing needs the appropriate connection permission and remains subject to your account's publishing access and the post's state.

### Codex

Add the hosted server:

```bash
codex mcp add risemore --url https://www.risemore.app/mcp
```

Complete the browser authorization if prompted. To authorize again or start login manually:

```bash
codex mcp login risemore
```

Check the configured connection with `codex mcp list`. Start a new Codex session if an existing session does not show the tools. See the [official Codex MCP documentation](https://learn.chatgpt.com/docs/extend/mcp?surface=cli).

### Cursor

Add this entry to `~/.cursor/mcp.json` for all projects, or `.cursor/mcp.json` for the current project. Merge it into the existing `mcpServers` object if other servers are already configured.

```json
{
  "mcpServers": {
    "risemore": {
      "url": "https://www.risemore.app/mcp"
    }
  }
}
```

Enable the server in Cursor's MCP settings and complete browser authorization. See the [official Cursor MCP documentation](https://cursor.com/docs/mcp).

### Claude Code

Add the connection for your user account:

```bash
claude mcp add --transport http --scope user risemore https://www.risemore.app/mcp
```

Open Claude Code, run `/mcp`, select `risemore`, and follow the authentication flow. See the [official Claude Code MCP documentation](https://code.claude.com/docs/en/mcp).

### Other clients

Use a client that supports remote MCP over Streamable HTTP with OAuth. Add the endpoint above, authorize your RiseMore account, and check that the tools appear.

## Available tools

| Read tool | What it provides |
| --- | --- |
| `list_products` | Your products and saved product context and research. |
| `list_channels` | Your publishing channels and connected accounts. |
| `list_posts` | Saved social posts, including drafts, scheduled posts, and published posts. |
| `get_post` | The content and details of a selected social post. |
| `list_materials` | Saved source material and research content. |
| `list_keywords` | Saved SEO keywords, scores, and opportunity reasons. |
| `list_reddit_threads` | Saved Reddit discussions, thread content, and comments. |
| `list_competitors` | Saved competitors and their research. |

Read tools return records belonging to the account you authorized. Start with `list_products`, then use the selected product's ID for product-specific requests.

| Publishing tool | What it does |
| --- | --- |
| `publish_now` | Publishes an already approved, scheduled social post through its connected channel, after your explicit confirmation. |

A read-only connection cannot publish. Review the post and destination before asking your client to use `publish_now`. This tool does not draft, edit, approve, or schedule a post; prepare those steps in the Console. See [Review & Publish](https://www.risemore.app/docs/review-and-publish).

Product setup, opportunity discovery, AI agent runs, content generation, editing, and SEO/GEO article publication happen in the Console. GEO monitoring is also available in the Console and has no MCP tool.

## Try a read request

```text
List my RiseMore products and read the latest saved product research.
```

```text
Show my active SEO keywords and explain their saved opportunity reasons.
```

```text
Show my scheduled social posts so I can review them. Do not publish anything.
```

## Reconnect an older installation

If you have an older VibeCom connection, add RiseMore with the server name `risemore` and the full endpoint `https://www.risemore.app/mcp`, then authorize it again. You can remove the old connection after the new one works.

If a product is missing, check that you authorized the RiseMore account that owns it. If tools do not appear, check the server is enabled and your client supports Streamable HTTP with OAuth, then reconnect or start a new session. Use your client's login flow again for authentication errors or missing permissions.

## Links

- [RiseMore website](https://www.risemore.app/)
- [Open Console](https://www.risemore.app/console)
- [MCP setup guide](https://www.risemore.app/docs/mcp-setup)
- [Quick Start](https://www.risemore.app/docs/quick-start)
- [Review & Publish](https://www.risemore.app/docs/review-and-publish)
- [Plans and pricing](https://www.risemore.app/pricing)
- [Support](https://www.risemore.app/support)
