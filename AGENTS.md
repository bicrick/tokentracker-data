# Agent guide: @bicrick's token usage

This repo holds @bicrick's AI coding token usage: daily totals per tool and model, per machine,
written by the tokentracker CLI. Do not edit files in `machines/` by hand.

## Answer questions from the static files (GitHub Pages, no server)

    https://bicrick.github.io/tokentracker-data/api/v1/stats.json        totals, active days, busiest day, streaks, today, this month, top tool and model
    https://bicrick.github.io/tokentracker-data/api/v1/usage.json        daily usage split by tool (also usage-week.json, usage-month.json)
    https://bicrick.github.io/tokentracker-data/api/v1/models.json       per model: tokens, responses, share, first/last used
    https://bicrick.github.io/tokentracker-data/api/v1/tools.json        per tool
    https://bicrick.github.io/tokentracker-data/api/v1/devices.json      per machine, last sync
    https://bicrick.github.io/tokentracker-data/api/v1/heatmap.json      calendar grid (also heatmap-365d.json, heatmap-90d.json)
    https://bicrick.github.io/tokentracker-data/api/v1/rows.json         every daily row      https://bicrick.github.io/tokentracker-data/api/v1/index.json   every file

Time ranges are folders: https://bicrick.github.io/tokentracker-data/api/v1/{ytd,30d,90d,365d}/<file>.json, e.g. https://bicrick.github.io/tokentracker-data/api/v1/30d/usage-week.json

For anything else (from/to dates, tools=a,b, models=x,y, group=, split=, format=csv), the query layer computes
from the same rows.json and stores nothing: https://tokentracker.patrickbrown.dev/api/v1/users/bicrick/usage?from=2026-11-01&group=week&split=tool
(resources: usage, models, tools, heatmap, stats, devices; profile at https://tokentracker.patrickbrown.dev/api/v1/users/bicrick)

Semantics: tokens = input + output + reasoning + cacheRead + cacheWrite. responses = model calls.
Dates are local days. Cursor has totals only (model "cursor/all"). Full reference:
https://tokentracker.patrickbrown.dev/llms.txt

## Keep it working

- A machine stopped syncing (an issue says so, or stats look stale): on that computer run
  `npx @bicrick/tokentracker@latest init --yes`. Safe to repeat; nothing is counted twice.
- Add another computer: run the same command there, signed into the same GitHub.
- Cursor: usage comes from the public profile cursor.com/@username, fetched by this repo's Action.
  If there is no Cursor data, ask the user whether they use Cursor and for their username, then run
  `npx @bicrick/tokentracker@latest connect --cursor <username>`.
- Data format: FORMAT.md. Stop syncing: `npx @bicrick/tokentracker uninstall`. Delete everything: delete this repo.
