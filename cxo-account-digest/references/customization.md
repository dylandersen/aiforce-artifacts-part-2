# Customizing the CXO Account Digest

Everything a customer tailors is in the `CONFIG` object at the top of the `<script>` in `assets/cxo-account-digest.html`. Leave the rest of the code alone unless a connector's response shape is different (see `data-contract.md`).

## CONFIG reference

| Key | Default | Change it when |
|---|---|---|
| `name` | `CXO Account Digest` | White-labelling the top bar, page title and footer |
| `locale`, `currency` | `en-US`, `USD` | Non-US reporting |
| `tools.*` | placeholders | Always: set the workspace's connector tool names |
| `apiVersion` | `v66.0` | The org's REST version differs |
| `sources` | all on | A connector isn't available, or the org doesn't use Cases. `ai:false` turns off synthesis and keeps the deterministic copy |
| `closedLookbackDays` | 365 | "Won" should cover the fiscal year instead |
| `signalWindowDays` | 90 | Long sales cycles (180) or high-velocity businesses (30) |
| `activityWindowDays` | 182 | Used for the 26-week heat ribbon; keep at 182 unless you change the bar count |
| `staleDealDays` | 45 | The definition of a "quiet" deal |
| `renewalWatchDays` | 120 | How far ahead a quiet renewal turns into a cooling signal |
| `vocab` | deal, deals, renewal | The org says opportunity, contract, engagement, policy, re-up… |
| `renewalTypePattern` | `/renew/i` | Renewals are marked differently (e.g. `/renew\|extension\|re-up/i`) |
| `lostStagePattern` | `/lost\|dead\|no decision\|no opportunity/i` | Closed-lost stage names differ |
| `execTitlePattern` | C-suite, president, founder, EVP/SVP/VP, head of, MD, GM | The industry has other senior titles (Dean, Provost, Chief Medical Officer, Superintendent, Partner) |
| `stageSegments` | 6 | Number of steps in the stage track |
| `industryLens` | empty | Always worth one sentence; see below |
| `sections` | 9 sections | Rename headers, reorder, or drop a section (also drop its render call) |

## Section headers

Headers do the explaining, so there's no helper text under them. Rename them in the customer's own language and keep each one a plain statement a skimming executive can act on.

```js
sections: [
  { key: "bottom",   label: "The bottom line",         icon: "compass" },
  { key: "matters",  label: "Why this matters",        icon: "target" },
  { key: "warming",  label: "What’s warming up",       icon: "flame", tone: "warm" },
  { key: "cooling",  label: "What’s cooling off",      icon: "snow",  tone: "cool" },
  { key: "deals",    label: "Deals in motion",         icon: "brief" },
  { key: "people",   label: "Who’s moving",            icon: "users" },
  { key: "voices",   label: "What the team is saying", icon: "chat" },
  { key: "calendar", label: "On the calendar",         icon: "cal" },
  { key: "moves",    label: "Your next move",          icon: "spark", tone: "warm" },
]
```

Icons are [Phosphor](https://phosphoricons.com) duotone (MIT), drawn in ink with no background tile; to add one, paste its duotone SVG body into a new `<symbol id="i-name" viewBox="0 0 256 256">` in the sprite at the bottom of the body. Available: search, cloud, slack, mail, cal, building, pin, user, users, userplus, swap, crown, flame, snow, up, down, alert, clock, target, renew, trophy, pulse, life, spark, compass, chat, brief, globe, quote, gauge.

## Industry examples

**Healthcare payer**
```js
vocab: { deal: "contract", deals: "contracts", renewal: "re-up" },
renewalTypePattern: /renew|re-?up|extension/i,
execTitlePattern: /\b(chief|ceo|cfo|cmo|cmio|cno|president|evp|svp|vp|vice president|medical director)\b/i,
industryLens: "Frame significance through member experience, star ratings, regulatory deadlines and cost of care.",
sections: [ …, { key: "deals", label: "Contracts in motion", icon: "brief" }, … ]
```

**Higher education**
```js
vocab: { deal: "initiative", deals: "initiatives", renewal: "renewal" },
execTitlePattern: /\b(president|provost|chancellor|dean|chief|cio|cfo|vice president|vp|registrar)\b/i,
industryLens: "Frame significance through enrolment, student success, retention and the academic calendar.",
```

**Manufacturing**
```js
vocab: { deal: "program", deals: "programs", renewal: "renewal" },
industryLens: "Frame significance through plant uptime, supply-chain risk, dealer network health and capital cycles.",
signalWindowDays: 180,
```

**Financial services**
```js
vocab: { deal: "mandate", deals: "mandates", renewal: "renewal" },
execTitlePattern: /\b(chief|ceo|cfo|cro|cio|coo|president|managing director|md|evp|svp|head of)\b/i,
industryLens: "Frame significance through AUM, wallet share, regulatory exposure and relationship depth.",
```

## Visual system

**Themes.** Four ship in the box, picked from the half-circle button in the top bar and remembered per viewer: Paper (cream, ember/glacier), Slate (white, `#56798E`), Emerald (off-white, emerald) and Mist (lavender-grey, plum). Each is one `[data-theme=…]` line of CSS variables; the `THEMES` array in the script lists them for the menu. To add a brand theme, copy a line, change the colours, and add `["key","Name","#swatch"]` to `THEMES`. Switching uses a circular reveal from the button (View Transitions API), and switches instantly when the viewer prefers reduced motion.

The design tokens are CSS variables in `:root`. The system has one rule: **temperature is the only colour.** Ember (`--ember`) means warming, glacier (`--glacier`) means cooling, brass (`--brass`) means steady or watch. Everything else is paper and ink.

- To re-brand, change `--ember` (and `--ember-wash`) to the customer's warm accent and `--glacier` to a cool counterpart. Keep the contrast on paper at 4.5:1 or better.
- The contour art (top bar mark, search page, candidate crests, masthead) is scaled to always fit its frame. The masthead picks one of 10 contour shapes (`VARIANTS`) at random each time a digest opens, and its colours follow the account’s temperature. Add or edit a row in `VARIANTS` to change the shapes.
- Typography: Newsreader for headlines and figures, Geist for UI text, Geist Mono for labels. All three are embedded as base64 WOFF2 and licensed under OFL 1.1.

## Scheduling

The artifact refreshes whenever it's opened, so no scheduled task is needed. To push a standing account to an executive each morning, schedule a task that opens the briefing in chat or posts a summary instead. The page itself never sends anything.
