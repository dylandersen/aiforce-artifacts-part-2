# Customizing the CFO Revenue Ledger

Everything a customer tailors is in `CONFIG` at the top of the script. Leave the core block alone unless a connector's response shape differs.

| Key | Default | Change it when |
|---|---|---|
| `locale`, `currency` | `en-US`, `USD` | Non-US reporting |
| `tools.*` | placeholders | Always |
| `apiVersion` | `v66.0` | The org's REST version differs |
| `renewalWhere` | `Type LIKE '%Renew%'` | How renewals are marked |
| `lostWhere` | `IsClosed = true AND IsWon = false AND (NOT StageName LIKE '%Duplicate%')` | What counts as a real loss |
| `quietDays` | `30` | Silence that counts as slip risk |
| `rows` | `8` | Ledger rows before "Show all" |
| `companyWide` | `regex` | Titles or roles that open on the whole company instead of their own team |
| `labels` | `…` | Every section header |

## Visual system

The palette, type and radius are CSS variables in `:root`. Change the accent variables to re-brand; keep text contrast at 4.5:1 or better. Fonts are embedded as base64 WOFF2 (OFL 1.1); icons are an inline Phosphor sprite, so adding one means pasting its SVG body into a new `<symbol id="i-name" viewBox="0 0 256 256">`.

Motion follows one rule set: entrances fade and rise a few pixels with a strong ease-out, numbers count up with tabular figures so widths don't jump, content swaps with a short blur crossfade that always clears, and everything collapses to instant when the viewer prefers reduced motion.
