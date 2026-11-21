# PivotBank MCP server

[![Listed on mcpservers.org](https://mcpservers.org/badge.svg)](https://mcpservers.org/servers/mgulraize/pivotbank-mcp)

Convert bank statement PDFs to Excel, CSV, QuickBooks (QBO), Xero (OFX), Quicken (QIF) or JSON from any MCP client, with every row checked against the statement's own running balances.

- **Endpoint:** `https://pivotbank.app/mcp` (streamable HTTP, stateless)
- **Docs server:** `https://pivotbank.app/mcp/docs` (no sign-in)
- **Registry name:** `app.pivotbank/pivotbank` in the [official MCP Registry](https://registry.modelcontextprotocol.io)
- **Website:** [pivotbank.app](https://pivotbank.app)

This repository holds the registry listing (`server.json`) and this guide. The server itself is hosted by PivotBank; there is nothing to install or run.

## Tools

| Tool | What it does | Sign-in |
| --- | --- | --- |
| `convert_statement` | Reads every transaction (date, description, money in, money out, balance), checks them against the running balances, and returns a link to download the statement as Excel, CSV, QBO, OFX, QIF or JSON. | PivotBank account, or a Pro API key |
| `check_statement_balances` | Says whether a statement adds up to the cent, and names the rows where it breaks. | Free PivotBank account |
| `summarise_spending` | Money in and out, spending by category, top merchants and repeating payments. | Free PivotBank account |
| `list_statements` | The statements saved on the user's account, newest first, each with its download link. | Free PivotBank account |
| `list_supported_banks` | The banks PivotBank recognises by name, for one country or all. A bank not listed still converts. | None |

The docs server has `search_docs` and `read_doc` for the API, auth, pricing and versioning.

## Connect

**Claude Code**

```bash
claude mcp add --transport http pivotbank https://pivotbank.app/mcp
```

**Claude Desktop, Cursor, Windsurf and other clients that take JSON**

```json
{
  "mcpServers": {
    "pivotbank": {
      "type": "http",
      "url": "https://pivotbank.app/mcp"
    }
  }
}
```

**VS Code** (`.vscode/mcp.json`)

```json
{
  "servers": {
    "pivotbank": {
      "type": "http",
      "url": "https://pivotbank.app/mcp"
    }
  }
}
```

The first call that needs an account opens PivotBank's sign-in (OAuth with PKCE). Agents without a browser can send a Pro API key instead: `Authorization: Bearer pvb_live_...`. Keys are made at [pivotbank.app/account/api-keys](https://pivotbank.app/account/api-keys).

## More

- [API guide](https://pivotbank.app/api-access) for the REST endpoint `POST /api/v1/convert`
- [OpenAPI spec](https://pivotbank.app/openapi.json)
- [Auth and error codes](https://pivotbank.app/auth.md)
- [llms.txt](https://pivotbank.app/llms.txt)
- Questions: contact@pivotbank.app

## Privacy

Statements are read to produce the conversion and are not used to train models. See [pivotbank.app/privacy](https://pivotbank.app/privacy).

## License

The contents of this repository (the listing and this guide) are MIT licensed. The PivotBank service is governed by its [terms](https://pivotbank.app/terms).
