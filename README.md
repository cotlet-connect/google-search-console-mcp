# How to connect Google Search Console to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Google Search Console account.** Google has not published its own Search Console app in the ChatGPT or Claude directories. Cotlet.dev connects your own signed-in Search Console account to any AI agent, so you can ask in plain words and the AI requests indexing and URL removals for you.

## What you can ask

> Request indexing for acmebakery.com/blog/holiday-cakes-2026 and the 3 product pages I published today.

> Remove acmebakery.com/old-menu-2024 from Google results and tell me when the request is submitted.

> Check which of my 12 blog posts from this week aren't indexed yet and request indexing for them.

> List every URL removal request I made in the last 30 days with its current status.

> Every Monday at 9 am, request indexing for the pages I updated the Friday before.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Google Search Console tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"google-search-console":{"command":"uvx","args":["google-search-console-cotlet-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t google-search-console-mcp .
docker run -i --rm -e COTLET_API_KEY google-search-console-mcp
```

Tools: `google_search_console_guide`, `google_search_console_status`, `google_search_console_open`, `google_search_console_read`, `google_search_console_click`, `google_search_console_type`, `google_search_console_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install google-search-console-cotlet-mcp        # or run it once: uvx google-search-console-cotlet-mcp connect
google-search-console-cotlet-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 google_search_console_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 google_search_console_agent.py status    # is Google Search Console ready in your Cotlet.dev account
python3 google_search_console_agent.py guide     # Google Search Console screens and sign-in link
python3 google_search_console_agent.py read      # open Google Search Console, read the page, close the browser
python3 google_search_console_agent.py tools     # list Cotlet.dev tools
python3 google_search_console_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Google Search Console users

**Does Google Search Console have an API?**

Google Search Console has an API, but it covers only part of the web interface (checked 16 Oct 2026). It offers Search Analytics queries (with an hourly breakdown for up to 10 days), sitemap list, get, submit and delete, property list, get, add and delete, and read-only URL Inspection of the indexed version. Cotlet.dev works in your own signed-in Google Search Console account, so your AI agent can request indexing and remove URLs with no API key and no code.

**How do I connect Google Search Console to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Google Search Console once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Google Search Console API key.

**Is there a way to use Claude with Google Search Console?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Google Search Console account.

**Is there a Google Search Console MCP server?**

Google has not published a Search Console connector in the ChatGPT or Claude directories, only third-party apps are listed there. Cotlet.dev is a hosted MCP server that works in Google Search Console for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Google Search Console on Cotlet.dev](https://cotlet.dev/integrations/google-search-console-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=google-search-console&utm_content=find)
- [PyPI package google-search-console-cotlet-mcp](https://pypi.org/project/google-search-console-cotlet-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-google-search-console-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/google-search-console-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=google-search-console

Start free: https://cotlet.dev/signup?app=google-search-console&utm_source=github&utm_medium=readme&utm_campaign=google-search-console
