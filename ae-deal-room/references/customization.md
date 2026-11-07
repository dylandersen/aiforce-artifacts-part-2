# Customizing the AE Deal Room

Everything a customer tailors is in `CONFIG` at the top of the script. Leave the core block alone unless a connector's response shape differs.

| Key | Default | Change it when |
|---|---|---|
| `locale`, `currency` | `en-US`, `USD` | Non-US reporting |
| `tools.*` | placeholders | Always |
| `apiVersion` | `v66.0` | The org's REST version differs |
| `quietDays` | `14` | Deal-level silence that counts as a risk |
| `engagedDays` | `30` | Window for a contact to count as engaged |
| `stallDays` | `30` | Days in one stage before it reads as stalled |
| `execTitle` | `regex` | Senior titles for the "executive in the room" check |
| `econRole` | `regex` | Contact roles that count as the economic buyer |
| `execLike` | `SOQL LIKE patterns` | Titles used to find senior contacts at the account for the drawer |
| `labels` | `…` | Every section header |

## Visual system

The palette, type and radius are CSS variables in `:root`. Change the accent variables to re-brand; keep text contrast at 4.5:1 or better. Fonts are embedded as base64 WOFF2 (OFL 1.1); icons are an inline Phosphor sprite, so adding one means pasting its SVG body into a new `<symbol id="i-name" viewBox="0 0 256 256">`.

Motion follows one rule set: entrances fade and rise a few pixels with a strong ease-out, numbers count up with tabular figures so widths don't jump, content swaps with a short blur crossfade that always clears, and everything collapses to instant when the viewer prefers reduced motion.
