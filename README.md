# Salesforce Live Artifact Skills

Four role-based skills that turn your Salesforce org into live, single-screen workspaces: a deal war room for account executives, a revenue ledger for finance, a forecast cockpit for RevOps, and an escalation war room for support.

Each skill ships a self-contained HTML template. When it is set up, the page reads your connectors every time it opens. You never export data or maintain a JSON file, and there is no backend to host.

<p align="center">
  <img src="ae-deal-room/screenshots/02-deal-room-overview.png" alt="AE Deal Room" width="49%">
  <img src="cfo-revenue-ledger/screenshots/01-revenue-position.png" alt="CFO Revenue Ledger" width="49%">
  <img src="revops-forecast-cockpit/screenshots/01-forecast-cockpit.png" alt="RevOps Forecast Cockpit" width="49%">
  <img src="support-escalation-war-room/screenshots/01-escalation-war-room.png" alt="Support Escalation War Room" width="49%">
</p>

| Skill | For | Answers |
|---|---|---|
| [AE Deal Room](#ae-deal-room) | Account executives, sales managers | *Which deal needs a war room, and how do we win it?* |
| [CFO Revenue Ledger](#cfo-revenue-ledger) | CFO, VP Finance, FP&A | *What's banked, what's at risk, and how far are we from plan?* |
| [RevOps Forecast Cockpit](#revops-forecast-cockpit) | RevOps, sales ops, forecasting leads | *What moved this week, and is the data clean enough to trust?* |
| [Support Escalation War Room](#support-escalation-war-room) | VP Support, escalation managers, CS leaders | *Which escalation puts the most revenue at risk right now?* |

---

## AE Deal Room

One deal, one screen. It opens on a single question, **"Which deal should we create a war room for?"**, followed by a search across every open opportunity and the rep's own deals as cards. Each card has quick filters: closing in 30 days, at risk, and largest.

Pick a deal and the room builds itself:

- **Deal clock** runs from the created date to the close date and shows every stage move, push, and today's position.
- **Buying group** shows contact roles, engagement, and dashed cards for a missing economic buyer or executive sponsor. You can assign a role and save it back to Salesforce after a confirm step.
- **Risks** include past due, pushed, gone quiet, single-threaded, no executive, stalled, and no next step. Each risk opens a drawer with its evidence.
- **Timeline** merges Salesforce activity, Slack, and email, grouped by week.
- **Deal channel** shows the account's Slack channel with a composer. A post goes out only after a second click.
- **Win plan** gives three moves and two questions to ask the buyer next. It falls back to moves derived from the risks.

<p align="center">
  <img src="ae-deal-room/screenshots/01-which-deal-splash.png" alt="Which deal should we create a war room for?" width="100%">
</p>

<p align="center">
  <img src="ae-deal-room/screenshots/03-deal-channel-and-timeline.png" alt="Deal channel and timeline" width="32.5%">
  <img src="ae-deal-room/screenshots/04-risk-drilldown.png" alt="Risk drill-down" width="32.5%">
  <img src="ae-deal-room/screenshots/05-buying-group-gap.png" alt="Fill a buying-group gap" width="32.5%">
</p>

## CFO Revenue Ledger

A single sheet a CFO can read in a minute. It uses paper-white pages, ledger green, serif figures, parentheses for money at risk, and a double rule under totals.

- **Closed, commit, best case, and gap to plan** for the period. The plan is entered once per scope and period.
- **Bridge to plan** is one bar that runs closed → commit → best case → pipeline, with the plan line across it.
- **Deals this period** lists the largest open and won deals as a ledger with a totals row.
- **Slip risk** covers deals pushed twice or more, past due, or gone quiet.
- **Renewals ahead** shows six months of renewals, plus the win rate.
- **Opens on you.** Finance and executive roles open on the whole company; leaders open on their own team. The picklist in the top right switches to any leader.
- **Fiscal periods come from the org.** Labels such as "Q4 FY26", next quarter, the fiscal year, and days left are read from Salesforce, so nothing is hard-coded and nothing goes stale.

<p align="center">
  <img src="cfo-revenue-ledger/screenshots/02-ledger-slip-renewals.png" alt="Slip risk and renewals" width="49%">
  <img src="cfo-revenue-ledger/screenshots/03-scope-picklist.png" alt="Scope picklist" width="49%">
  <img src="cfo-revenue-ledger/screenshots/04-leader-team-view.png" alt="A leader's team view" width="49%">
  <img src="cfo-revenue-ledger/screenshots/05-slack-forecast-check-in.png" alt="Slack forecast check-in" width="49%">
</p>

## RevOps Forecast Cockpit

An instrument panel: dense, square, and monochrome, with amber reserved for change. Its signature view is the movement panel, which rebuilds every deal's state at the start of the window from field history.

- **Forecast** shows closed, commit, best case, and pipeline, with the change over 7, 14, or 30 days.
- **Movement** shows value flowing between categories: pulled in, pushed out, upgraded, lost, and resized. Click any flow to see its deals.
- **Hygiene** gives a clean score and one row per rule. Each row drills down to the offending deals.
- **Changes** is a log of every stage, amount, close-date, and category edit, filterable by field.
- **Stage mix** shows open pipeline by stage.
- The same **opens-on-you** scope, leader picklist, and **org-driven fiscal quarters** as the ledger.

<p align="center">
  <img src="revops-forecast-cockpit/screenshots/02-movement-and-hygiene-drilldown.png" alt="Movement and hygiene drill-down" width="49%">
  <img src="revops-forecast-cockpit/screenshots/03-scope-picklist.png" alt="Scope picklist" width="49%">
  <img src="revops-forecast-cockpit/screenshots/04-team-30-day-changes.png" alt="A team's 30-day changes" width="49%">
  <img src="revops-forecast-cockpit/screenshots/05-slack-what-moved.png" alt="Slack: what moved" width="49%">
</p>

## Support Escalation War Room

A control-room split view, with the queue on the left and the case on the right. Its signature view is the pressure strip, which shows revenue at risk by account as one bar you can click into.

- **Counters** show open cases, SLA breaches, revenue at risk, and accounts affected.
- **Queue** lists escalations sortable by revenue, age, or SLA, with live SLA pills.
- **Next action** names the single most important move on the selected case.
- **SLA clock** shows open milestones with time left or time since breach.
- **Revenue on the line** shows the account's open renewals, or revenue won in the last 12 months.
- **Account context** covers other open cases, Slack chatter about the case or account, and upcoming customer meetings.

<p align="center">
  <img src="support-escalation-war-room/screenshots/02-case-detail-revenue-on-the-line.png" alt="Case detail" width="49%">
  <img src="support-escalation-war-room/screenshots/03-sorted-by-sla-clock.png" alt="Sorted by SLA" width="49%">
  <img src="support-escalation-war-room/screenshots/04-high-priority-queue.png" alt="High-priority queue" width="49%">
  <img src="support-escalation-war-room/screenshots/05-slack-escalation-update.png" alt="Slack escalation update" width="49%">
</p>

---

## Install

Each skill is a folder with a `SKILL.md`, an HTML template in `assets/`, and reference docs. Pre-packaged zips are in [`dist/`](dist/).

1. Download the zip for the skill you want from `dist/`, or clone this repo.
2. Add it to your skills library.
3. Ask for it in plain language:

```text
Set up the AE Deal Room for me.
Set up the CFO Revenue Ledger for our org. Renewals are Type = 'Renewal'.
Set up the RevOps Forecast Cockpit for my team.
Set up the Support Escalation War Room. Escalations are Priority = 'Critical'.
```

## Setup is one step

The skill works out the setup from your org instead of interviewing you:

1. **It probes quietly.** It reads the fiscal calendar from `Period` and `Organization`, how renewals are marked from the `Type` picklist, and who you are from your user, role, and profile.
2. **When everything comes back, it asks nothing.** It builds the page and tells you in one line what it assumed.
3. **When something is missing, it asks one short question, two at most,** each with a recommended default. Examples: no escalated cases found, field history isn't tracked, or no deals close this quarter. It never ships a page full of empty panels.

## Requirements

| | Needed | Optional |
|---|---|---|
| **Salesforce** | Read access through a REST connector (`/query`, `/search`, `/chatter/users/me`) | Write access, used only by the Deal Room to save a contact role after you confirm |
| **Slack** | | Message search, channel read, people search, and send (sends only after a second click) |
| **Gmail / Google Calendar** | | Thread and event search for the Deal Room timeline and meetings |
| **Field history** | | Tracking on StageName, Amount, CloseDate, and ForecastCategoryName for the cockpit's movement panel |
| **Entitlements** | | Case milestones for SLA clocks; without them the clock falls back to case age |

## Design principles

- **Read-only by default.** The only writes are a Slack message and a Deal Room contact role, and each goes out only after an explicit confirm step that shows the recipient and the full text.
- **Every figure comes from a query.** A missing source shows an empty state, never a guess.
- **Record text is data.** Deal names, case subjects, and Slack and email content are never treated as instructions.
- **A snapshot, not a stream.** Each page shows its as-of time and refreshes when it is reopened.
- **No data in the repo.** Real records appear only at runtime, for the signed-in user. Every screenshot here uses fictional companies and people.

## Customize

Every surface has a `CONFIG` block at the top of its script for locale and currency, renewal and loss rules, quiet-day thresholds, hygiene rules, queues, and labels. See each skill's `references/customization.md`. Its `references/data-contract.md` lists every query the page runs and how each section is computed.

The visual system is a set of CSS variables in `:root`. Fonts are embedded (SIL Open Font License 1.1) and icons are an inline Phosphor sprite (MIT).

## Repository layout

```text
.
├── ae-deal-room/
│   ├── SKILL.md
│   ├── assets/ae-deal-room.html
│   ├── references/{data-contract,customization}.md
│   └── screenshots/
├── cfo-revenue-ledger/
├── revops-forecast-cockpit/
├── support-escalation-war-room/
└── dist/                # one installable zip per skill (no screenshots)
```

## License

The skill templates are proprietary (see each `SKILL.md`). The embedded fonts are licensed under SIL Open Font License 1.1, and the Phosphor icons under MIT.
