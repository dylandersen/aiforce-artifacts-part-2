# AIforce Artifacts for Claude: Part 2

Five live Salesforce artifacts for **Claude Desktop**: a deal war room for AEs, a revenue ledger for finance, a forecast cockpit for RevOps, an escalation war room for support, and an executive account digest for CXOs. Each reads your connectors every time it opens. No exports, no backend.

<p align="center">
  <img src="cxo-account-digest/screenshots/01-which-account-splash.png" alt="CXO Account Digest" width="100%">
</p>

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
| [CXO Account Digest](#cxo-account-digest) | CEO, CRO, COO, executive sponsors, account leaders | *Which account should we look up, and what do I need to know before the meeting?* |

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

## CXO Account Digest

A search, confirm, brief workspace for executives. It opens on one question, **"Which account should we look up?"**, then briefs you on the account you pick.

- **Search and confirm** finds candidate accounts in Salesforce and shows industry, HQ, owner, last activity, and open pipeline, so duplicate records are easy to tell apart.
- **Briefing** fills in as data arrives: bottom line, why it matters, what's warming up, what's cooling off, deals in motion, and who's moving.
- **Conversations** pull in what the team is saying in Slack and email, plus upcoming meetings from your calendar.
- **Next moves** and questions to ask come from a Claude-written synthesis of the sources above.
- **Read-only.** It only queries your connectors, and remembers recent accounts per viewer.

<p align="center">
  <img src="cxo-account-digest/screenshots/01-which-account-splash.png" alt="Which account should we look up?" width="49%">
  <img src="cxo-account-digest/screenshots/02-confirm-account.png" alt="Confirm the account" width="49%">
  <img src="cxo-account-digest/screenshots/03-digest-bottom-line.png" alt="Digest bottom line" width="49%">
  <img src="cxo-account-digest/screenshots/04-next-move-and-questions.png" alt="Next moves and questions to ask" width="49%">
</p>

---

## Set up in Claude Desktop

1. Download a zip from [`dist/`](dist/), such as `ae-deal-room.zip`.
2. In Claude Desktop, open **Settings → Capabilities → Skills** and choose **Upload skill**. Select the zip, then switch the skill on.
3. Start a chat and ask for it:

```text
Set up the AE Deal Room for me.
Set up the CFO Revenue Ledger for our org. Renewals are Type = 'Renewal'.
Set up the RevOps Forecast Cockpit for my team.
Set up the Support Escalation War Room. Escalations are Priority = 'Critical'.
Set up the CXO Account Digest for me.
```

Claude probes your org for the fiscal calendar, renewal marking and your role, then builds the artifact. It asks at most two short questions, only when something is missing. Reopen the artifact any time to refresh it.

## Connectors

Connect these in Claude Desktop under **Settings → Connectors** first.

- **Salesforce MCP** (required): read access. Write access is used only to save a Deal Room contact role.
- **Slack MCP**: Slack search, channel read, and posting.
- **Email and calendar**: any mail and calendar connector, for timelines and meetings.

Optional org features: field history on StageName, Amount, CloseDate and ForecastCategoryName (cockpit movement), and Entitlements (SLA clocks).

Every figure comes from a query, and writes (a Slack post or a contact role) happen only after an explicit confirm. All screenshots use fictional data.

## Customize

Each skill has a `CONFIG` block for locale, currency and thresholds. See `references/customization.md` and `references/data-contract.md`.

## License

Proprietary (see each `SKILL.md`). Fonts: SIL OFL 1.1. Icons: Phosphor (MIT).
