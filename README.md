# FTA MCP: Fantasy Football, NBA, MLB and NHL Fantasy and DFS Data in Claude and ChatGPT

Fantasy Team Advice (FTA) runs a paid, hosted MCP connector. Add it to Claude, ChatGPT or another MCP app and your assistant can look up FTA's NFL, NBA, MLB and NHL fantasy and DFS data: props, projections, DraftKings and FanDuel slates, DFS ownership, NFL draft rankings, player pages and stats. Connecting requires an FTA membership with AI access.

Updated 2026-11-17

## Server URL and how to connect

Server URL:

```
https://mcp.fantasyteamadvice.com/mcp
```

Paste it exactly, with no trailing slash and no spaces. Sign-in uses OAuth: the app opens fantasyteamadvice.com, you log in with your FTA account, and you click Authorize. Menu names change between app releases, so the server URL and the Authorize button are what to look for.

### Claude (claude.ai and the desktop app)

1. Open Settings, then under Customize open Connectors, then click Add.
2. Name it FTA and paste the server URL into Remote MCP server URL. Click Continue.
3. Leave the authentication options Claude has marked Detected as they are, then click Add.
4. Click Connect, log in to FTA if asked, and click Authorize.
5. In a chat, choose Always allow the first time Claude asks to use an FTA tool.

### ChatGPT (paid plan)

1. Turn on Developer mode: Settings, then Security and login, then scroll to the bottom.
2. In Settings open Plugins, then in the main menu open Plugins and click the + button.
3. Name it FTA, leave Connection on Server URL, paste the server URL, and leave Authentication on OAuth.
4. Tick the acknowledgement box, click Create, then Sign in with FTA and Authorize.
5. In a new chat, click the + at the left of the message box and switch FTA on.

### Claude Code

```
claude mcp add --transport http fta https://mcp.fantasyteamadvice.com/mcp
```

Start Claude Code, run `/mcp`, select fta, choose Authenticate, log in to FTA in the browser and click Authorize.

### Gemini CLI

```
gemini mcp add --transport http fta https://mcp.fantasyteamadvice.com/mcp
```

Start `gemini`, run `/mcp` to confirm fta is listed, and ask a question. The first time, the browser opens so you can log in to FTA and click Authorize. The Gemini app at gemini.google.com does not take custom MCP servers; the Gemini CLI does.

### Cursor

Open Cursor Settings, choose MCP, then Add new MCP server with the URL type, or paste this into `mcp.json`:

```json
{
  "mcpServers": {
    "fta": {
      "url": "https://mcp.fantasyteamadvice.com/mcp"
    }
  }
}
```

Cursor opens your browser: log in to FTA and click Authorize. Use the chat pane in Agent mode.

### Grok, Perplexity and Le Chat

Each has a custom connector screen on a paid plan that supports it.

- Grok: grok.com/connectors, New Connector, Custom.
- Perplexity: Settings, Connectors, Add Connector, then the custom or advanced option.
- Le Chat: Intelligence, Connectors, Add connector, then the Add custom connector tab.

In all three, name it FTA, paste the server URL, pick Streamable HTTP if asked for a transport, then Connect, log in to FTA and click Authorize.

### Other MCP apps (VS Code, Windsurf, Zed, Raycast and more)

Add a remote server (HTTP, Streamable HTTP or URL, not a command or stdio server), name it `fta`, paste the server URL, then log in to FTA in the browser window and click Authorize.

## Tools (40)

There are 40 tools, and 38 of them are read-only. The other two, `file_feature_request` and `reply_to_support_ticket`, write a support ticket or a ticket reply, and only when you ask the assistant to. The connector cannot place bets, enter contests or change your account.

### Players, news and injuries

- `search_players`: finds players by name and returns the id other tools need.
- `get_player_page`: reads one tab of a player page, such as game log, splits, props, contract or news.
- `get_player_news`: lists the latest news for a player, a team or a position, newest first.
- `get_team_inactives`: gives a team's current injury report, split by status.
- `get_nba_injury_report`: lists every NBA player on the injury report with status, injury and return date when one is listed.

### Player props and futures

- `get_player_props`: lists sportsbook prop lines by market, with the line and the over and under prices.
- `get_prop_ev`: ranks today's prop lines by the edge and expected value FTA projects.
- `get_season_long_props`: lists season-long NFL player markets such as MVP and Rookie of the Year, with prices.
- `get_team_futures`: lists NFL team futures: Super Bowl, conference and division winners, and win totals.

### Projections, matchups and lineups

- `get_projections`: gives projected fantasy points for every player on a slate, with ceiling, floor and value.
- `get_start_sit`: compares two NFL players for the same week and says who to start.
- `get_defense_vs_position`: shows how every NFL defense has done against each position, week by week.
- `get_strength_of_schedule`: ranks NFL teams by how easy or hard their schedule is for a position.
- `get_nba_team_usage`: shows NBA usage rates for a team, with or without chosen players on the floor.
- `get_nba_efficiency_ratings`: lists the main slate's NBA efficiency ratings for each player.
- `get_nba_lineups`: shows each NBA game's starting five per team, whether the lineup is confirmed, expected or projected, and who is out.
- `get_nhl_lineups`: shows each NHL team's starting goalie, forward lines, defense pairs and power-play units.

### DFS slates and lineups

- `get_dfs_slates`: lists the DraftKings and FanDuel slates loaded for a date, main and showdown.
- `get_dfs_slate_players`: returns every player on one slate with salary, position and projection.
- `get_dfs_optimizer_data`: gives the inputs FTA's optimizer builds lineups from for one slate.
- `simulate_lineups`: simulates up to ten lineups on one slate and shows how each one tends to finish.
- `get_dfs_slate_export`: gives a short-lived download link for a slate's full player pool as a CSV file.

### DFS ownership

- `get_ownership_projections`: shows the tournament ownership FTA projects for every player on a slate.
- `get_ownership_history`: shows how owned a player was on past slates, next to what FTA had projected.
- `get_ownership_accuracy`: reports how close FTA's ownership projections were on settled slates.

### Past contests

- `get_contest_slates`: lists the past slates that have real contest results for a date.
- `get_contests`: lists past DFS contests with entries, prize pool and winning score, biggest first.
- `get_contest_ownership`: shows the ownership every player actually drew in a finished contest.
- `get_dfs_history_export`: gives download links for ownership history files that cover a range of dates.

### NFL draft

- `get_draft_rankings`: returns FTA's own NFL draft rankings by value over replacement, for your scoring settings.
- `get_adp`: gives the market's average draft position for NFL players.
- `get_auction_values`: gives the auction dollar value FTA suggests for each NFL player.

### Scores and stats

- `get_scores`: returns live and final scores for a day, or for an NFL week.
- `get_box_score`: shows every player's line from a single game. NHL has no player box score.
- `get_stat_leaders`: ranks players or teams on a season stat.
- `get_nfl_advanced_stats`: ranks NFL players and defenses on tracking-data and play-by-play stats.

### Site map and support

- `get_site_map`: lists what the server can answer, with every tool and every player page tab.
- `get_support_tickets`: lists your own FTA support tickets and their status.
- `file_feature_request`: files a support ticket asking for a missing feature or data set. It writes a ticket.
- `reply_to_support_ticket`: adds a reply to one of your own support tickets. It writes a reply.

## Example questions

- "Who is the highest-owned player on Sunday's main slate, and how accurate has FTA's ownership projection been lately?" (`get_ownership_projections`, `get_ownership_accuracy`)
- "Give me the top 10 running backs left by VBD in a 12-team PPR league." (`get_draft_rankings`)
- "Should I start Chris Olave or Garrett Wilson this week?" (`get_start_sit`)
- "Who is starting in goal for each NHL team tonight?" (`get_nhl_lineups`)
- "How owned was Nikola Jokic over his last ten NBA slates?" (`get_ownership_history`)

## Price

The Annual + AI + Historical Data plan is $199.99 a year. A monthly plan with AI access is $59.99 a month. You need a membership to connect. Current plans and checkout: https://fantasyteamadvice.com/memberships

## Learn more

- Fantasy football MCP: https://fantasyteamadvice.com/fantasy-football-mcp
- Fantasy basketball MCP: https://fantasyteamadvice.com/fantasy-basketball-mcp
- Fantasy baseball MCP: https://fantasyteamadvice.com/fantasy-baseball-mcp
- Every tool, with an example question: https://fantasyteamadvice.com/fantasy-mcp-tools
- Site: https://fantasyteamadvice.com
- For sportsbook and prediction-market odds comparison, see BeatVig: https://beatvig.com/

## This repository

This repository is documentation only. Fantasy Team Advice hosts the MCP server behind a paid FTA login, so there is no code here to install or run. Support: https://fantasyteamadvice.com/contact_us
