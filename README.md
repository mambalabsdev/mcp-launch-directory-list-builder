# Launch Directory List Builder MCP Server

An MCP server for the Mamba Labs Launch Directory List Builder actor on Apify. Describe what you are launching and get a ranked list of places to submit it, each checked live today.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

The places (directories, launch sites, newsletters, communities, subreddits, marketplaces, press and review pages, and curated GitHub lists) come from the public domain awesome-submitlist catalog, read fresh on every run. Each row carries the submission link, price, link type, audience, rules, and a fit score against your description. The actor checks each submission page live, with robots.txt obeyed: up, moved to another site, parked, gone, login first, submit form found, prices shown, and the newest date on the page. A Tranco popularity rank is added per site. One free summary row closes each run.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-launch-directory-list-builder": {
      "command": "npx",
      "args": ["-y", "@mambalabsdev/mcp-launch-directory-list-builder"],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `build_launch_directory_list` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Where should I launch my AI meeting notes tool for sales teams? Give me the 25 best fits."
- "List free directories that give a dofollow link, and check which ones are still up."
- "Which launch sites have a submit form and showed activity this month?"

## Tool

`build_launch_directory_list`. One tool. Example arguments:

```json
{
  "product_description": "AI meeting notes tool for B2B sales teams",
  "categories": [
    "saas",
    "ai"
  ],
  "max_rows": 25
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `product_description` | string | no | What you are launching and who it is for. |
| `categories` | array | no | ai, analytics, business, community, design, developer-tools, ecommerce, indie, marketing, productivity, saas, social, software, startup. |
| `keywords` | array | no | Extra words to score places by. |
| `types` | array | no | directory, product-launch-site, newsletter, community, subreddit, marketplace, citation, github. Default all but github. |
| `free_only` | boolean | no | Places marked free only. Default false. |
| `dofollow_only` | boolean | no | Places marked dofollow only. Default false. |
| `min_fit_score` | integer | no | Minimum fit score, 0 to 100. Default 0. |
| `check_live` | boolean | no | Check each page today. Default true. |
| `include_rank` | boolean | no | Add the Tranco rank. Default true. |
| `max_rows` | integer | no | Place rows per run. Default 100. |
| `only_new` | boolean | no | Skip places an earlier run returned. Default false. |
| `state_key` | string | no | Name for the only new places memory. |
| `max_charge_usd` | string | no | Optional cost cap for the run. |
| `proxy_mode` | string | no | auto or direct. Default auto. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `destination-row`, per place delivered | $0.005 | $0.00475 | $0.0045 | $0.00425 |
| `apify-actor-start`, per run start | $0.0015 | $0.0015 | $0.0015 | $0.0015 |

The run summary row, input refusal rows, places whose page the live check could not read, and places skipped with only_new are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/launch-directory-list-builder](https://apify.com/mambalabs/launch-directory-list-builder)

## License

MIT. See [LICENSE](LICENSE).
