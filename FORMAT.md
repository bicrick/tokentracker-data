# tokentracker data format

Written by the tokentracker CLI. Plain JSON, safe to read with anything.

## Layout

    tokentracker.json                 settings: { "format": 1, "cursorHandle": "name" | null }
    machines/<machine-id>/<year>.json  one file per computer per calendar year
    .github/workflows/tokentracker.yml builds the static API on GitHub Pages

`<machine-id>` is a one-way hash of the computer's hardware id, so the same computer
always writes the same files even if it is renamed or set up again.

## Machine file (format 1)

    {
      "format": 1,
      "machine": "<machine-id>",
      "device": "my-laptop",            // display name, may change
      "year": 2026,
      "syncedOn": "2026-11-19",         // last day this machine synced (written at least daily)
      "updatedAt": "2026-11-19T18:00:00Z", // last time any number changed
      "rows": [
        { "date": "2026-11-19", "source": "claude-code", "model": "anthropic/claude-opus-5-5",
          "input": 0, "output": 0, "reasoning": 0, "cacheRead": 0, "cacheWrite": 0, "messages": 0 }
      ]
    }

- `date` is a local calendar day on that machine. One row per (date, source, model).
- `tokens` = input + output + reasoning + cacheRead + cacheWrite. `messages` counts model responses.
- Rows are only ever added or updated, never removed: tools delete old logs, history stays here.

## Compatibility promise

Future versions only add fields or new format numbers. Every tokentracker release reads every
format ever written. If tokentracker disappears, this data and this description still work.
