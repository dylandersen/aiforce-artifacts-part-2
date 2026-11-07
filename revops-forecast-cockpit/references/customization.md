# Customizing the RevOps Forecast Cockpit

Everything a customer tailors is in `CONFIG` at the top of the script. Leave the core block alone unless a connector's response shape differs.

| Key | Default | Change it when |
|---|---|---|
| `locale`, `currency` | `en-US`, `USD` | Non-US reporting |
| `tools.*` | placeholders | Always |
| `apiVersion` | `v66.0` | The org's REST version differs |
| `checks` | `5 rules` | Hygiene rules as [label, SOQL condition] |
| `maxMoved` | `400` | Deals scanned for movement |
| `companyWide` | `regex` | Titles or roles that open on the whole company instead of their own team |
| `labels` | `…` | Every panel header |

## Visual system

The palette, type and radius are CSS variables in `:root`. Change the accent variables to re-brand; keep text contrast at 4.5:1 or better. Fonts are embedded as base64 WOFF2 (OFL 1.1); icons are an inline Phosphor sprite, so adding one means pasting its SVG body into a new `<symbol id="i-name" viewBox="0 0 256 256">`.

Motion follows one rule set: entrances fade and rise a few pixels with a strong ease-out, numbers count up with tabular figures so widths don't jump, content swaps with a short blur crossfade that always clears, and everything collapses to instant when the viewer prefers reduced motion.
