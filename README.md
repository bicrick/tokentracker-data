<p align="center">
  <a href="https://tokentracker.patrickbrown.dev/u/bicrick"><img src="https://raw.githubusercontent.com/bicrick/tokentracker/main/docs/assets/banner.png" alt="tokentracker" width="100%"></a>
</p>

<p align="center">
  ![tokens this year](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fbicrick.github.io%2Ftokentracker-data%2Fapi%2Fv1%2Fytd%2Fstats.json&query=%24.display.tokens&label=tokens%20this%20year&color=f0c463&style=flat-square&cacheSeconds=3600)
  ![active days](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fbicrick.github.io%2Ftokentracker-data%2Fapi%2Fv1%2Fytd%2Fstats.json&query=%24.display.activeDays&label=active%20days&color=6b9eff&style=flat-square&cacheSeconds=3600)
  ![current streak](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fbicrick.github.io%2Ftokentracker-data%2Fapi%2Fv1%2Fstats.json&query=%24.display.currentStreak&label=current%20streak&color=6b9eff&style=flat-square&cacheSeconds=3600)
</p>

<p align="center">
  <a href="https://tokentracker.patrickbrown.dev/u/bicrick">Profile</a> ·
  <a href="https://tokentracker.patrickbrown.dev/api/v1/users/bicrick">API</a> ·
  <a href="https://bicrick.github.io/tokentracker-data/api/v1/index.json">Static API</a> ·
  <a href="FORMAT.md">Data format</a>
</p>

---

**@bicrick's AI coding token usage**, tracked by [tokentracker](https://github.com/bicrick/tokentracker) across every tool and every machine. This repo is the database: plain JSON, owned by @bicrick. Only daily token counts per tool and model are stored, never prompts, code, paths or keys.

## Query it

```sh
curl https://tokentracker.patrickbrown.dev/api/v1/users/bicrick/stats
curl "https://tokentracker.patrickbrown.dev/api/v1/users/bicrick/usage?range=30d&group=week"
```

| Static JSON (GitHub Pages, no server) | |
|---|---|
| [`stats.json`](https://bicrick.github.io/tokentracker-data/api/v1/stats.json) | totals, streaks, busiest day, top tool and model |
| [`usage.json`](https://bicrick.github.io/tokentracker-data/api/v1/usage.json) · [`usage-month.json`](https://bicrick.github.io/tokentracker-data/api/v1/usage-month.json) | usage over time, split by tool |
| [`30d/usage.json`](https://bicrick.github.io/tokentracker-data/api/v1/30d/usage.json) | also `ytd/`, `90d/`, `365d/` |
| [`models.json`](https://bicrick.github.io/tokentracker-data/api/v1/models.json) · [`tools.json`](https://bicrick.github.io/tokentracker-data/api/v1/tools.json) | per model and per tool |
| [`heatmap.json`](https://bicrick.github.io/tokentracker-data/api/v1/heatmap.json) | ready-to-render calendar |
| [`index.json`](https://bicrick.github.io/tokentracker-data/api/v1/index.json) | everything |

## Layout

```
machines/<machine>/<year>.json   one file per computer per year (written by the CLI)
tokentracker.json                settings
.github/workflows/               rebuilds the static API on every change
```

Set up your own: `npx @bicrick/tokentracker init`. Stop on a machine: `npx @bicrick/tokentracker uninstall`. Delete everything: delete this repo.
