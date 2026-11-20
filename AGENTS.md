# Agent guide: @bicrick's token usage

This repo holds @bicrick's AI coding token usage: daily totals per tool and model, per machine,
written by the tokentracker CLI. Do not edit files in `machines/` by hand.

## Answer questions with the API (no auth, GET, JSON)

    https://tokentracker.patrickbrown.dev/api/v1/users/bicrick                  profile and links
    https://tokentracker.patrickbrown.dev/api/v1/users/bicrick/stats            totals, active days, busiest day, streaks, today, this month, top tool and model
    https://tokentracker.patrickbrown.dev/api/v1/users/bicrick/usage            time series: group=day|week|month|year|total, split=tool|model
    https://tokentracker.patrickbrown.dev/api/v1/users/bicrick/models           per model: tokens, responses, share, first/last used
    https://tokentracker.patrickbrown.dev/api/v1/users/bicrick/tools            per tool
    https://tokentracker.patrickbrown.dev/api/v1/users/bicrick/heatmap          calendar grid (range=year|365d|90d)
    https://tokentracker.patrickbrown.dev/api/v1/users/bicrick/devices          per machine, last sync

Filters on all: range=all|ytd|Nd|YYYY, from=YYYY-MM-DD, to=YYYY-MM-DD, tools=a,b, models=x,y,
format=csv (usage, models, tools, devices). Example: `https://tokentracker.patrickbrown.dev/api/v1/users/bicrick/usage?range=30d&group=week&split=tool`

The same data as static files, with no tokentracker server involved:

    https://bicrick.github.io/tokentracker-data/api/v1/stats.json  usage.json  usage-week.json  usage-month.json  models.json  tools.json
    https://bicrick.github.io/tokentracker-data/api/v1/devices.json  heatmap.json  profile.json  rows.json (every row)  index.json
    https://bicrick.github.io/tokentracker-data/api/v1/{ytd,30d,90d,365d}/<same>.json

Semantics: tokens = input + output + reasoning + cacheRead + cacheWrite. responses = model calls.
Dates are local days. Cursor has totals only (model "cursor/all"). Full reference:
https://tokentracker.patrickbrown.dev/llms.txt

## Keep it working

- A machine stopped syncing (an issue says so, or stats look stale): on that computer run
  `npx @bicrick/tokentracker@latest init --yes`. Safe to repeat; nothing is counted twice.
- Add another computer: run the same command there, signed into the same GitHub.
- Change the Cursor profile: `npx @bicrick/tokentracker connect` (or edit cursorHandle in tokentracker.json).
- Data format: FORMAT.md. Stop syncing: `npx @bicrick/tokentracker uninstall`. Delete everything: delete this repo.
