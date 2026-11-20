# tokentracker data

My AI coding token usage, collected by [tokentracker](https://github.com/bicrick/tokentracker).
This repo is the whole database: plain JSON I own. See [FORMAT.md](FORMAT.md).

| | |
|---|---|
| Full API (any filter, CSV) | https://tokentracker.patrickbrown.dev/api/v1/users/bicrick |
| Static API (GitHub Pages) | https://bicrick.github.io/tokentracker-data/api/v1/index.json |
| Stats | https://bicrick.github.io/tokentracker-data/api/v1/stats.json |
| Last 30 days | https://bicrick.github.io/tokentracker-data/api/v1/30d/usage.json |
| Heatmap | https://bicrick.github.io/tokentracker-data/api/v1/heatmap.json |

Only daily token counts per tool and model are stored: never prompts, code, paths or keys.
To stop: run `npx @bicrick/tokentracker uninstall` on each machine. To delete everything: delete this repo.
