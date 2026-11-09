# CXO Account Digest: data contract

The page builds every number from the queries below at view time. Nothing is stored except a per-viewer "recent accounts" list in `localStorage`.

## Contents
- Probe calls
- Salesforce queries
- External sources
- How each section is computed
- Synthesis contract

## Probe calls

Run each of these once in chat before publishing and compare the shape.

| Source | Call | Shape the parser expects |
|---|---|---|
| Salesforce | `{url:"/services/data/v66.0/query", method:"GET", queryParams:{q:"SELECT Id, Name FROM Account LIMIT 1"}}` | `{status_code, body:{records:[…]}, url}` (`url` is used to build record links) |
| Salesforce | `{url:"/services/data/v66.0/search", method:"GET", queryParams:{q:"FIND {Acme*} IN NAME FIELDS RETURNING Account(Id, Name)"}}` | `{status_code, body:{searchRecords:[…]}}` |
| Slack | `{keywords:["Acme"], limit:5, sort:"timestamp", response_format:"detailed", include_context:false}` | `{results:"markdown"}` with `### Result n of m` blocks containing `Channel:`, `From:`, `Time: YYYY-MM-DD HH:MM:SS TZ`, `Permalink: [link](url)`, `Text:` |
| Gmail | `{query:"\"Acme\" newer_than:90d", pageSize:5, view:"THREAD_VIEW_SUMMARY"}` | `{threads:[{viewUrl, messageCount, messages:[{subject, sender, date, snippet, addressDisplayNames}]}]}` (`{}` means none) |
| Calendar | `{query:"Acme", pageSize:5}` | `{events:[{summary, start:{dateTime}, htmlLink, attendees:[{email, self, resource}], attachments}]}` |

If a connector differs, change only its loader (`sfGet`, `loadSlack`, `loadMail`, `loadCalendar`) so it returns the same normalized objects.

## Salesforce queries

`{id}` is the confirmed Account Id (validated against `^[a-zA-Z0-9]{15,18}$`). Windows come from `CONFIG`.

| Key | Object | Purpose | Blocking |
|---|---|---|---|
| search | Account (SOSL, SOQL `LIKE` fallback) | Candidates | yes |
| candidate pipeline | Opportunity aggregate `COUNT(Id)`, `SUM(Amount)` open, grouped by AccountId | Tell duplicates apart | no |
| acct | Account | Masthead | pass 1 |
| opps | Opportunity: open, plus closed in `closedLookbackDays` | Ledger, deals, signals | pass 1 |
| contacts | Contact (200 by last activity) | Executive bench | pass 1 |
| newContacts | Contact created in `signalWindowDays` | New faces | pass 1 |
| tasks | Task `ActivityDate, CreatedDate` in `activityWindowDays` | Engagement heat | pass 1 |
| events | Event `Subject, StartDateTime` past and next 60 days | Heat, meetings | pass 1 |
| cases | Case open or recent (if `sources.cases`) | Escalation signal | pass 1 |
| hist | OpportunityFieldHistory: StageName, Amount, CloseDate | Advanced, slipped, resized | enrich, 30 s timeout |
| titleMoves | ContactHistory: Title | Changing seats | enrich, 30 s timeout |

Field history must be enabled on those fields for the history signals to appear. Without it the page still works and those signals stay quiet.

## External sources

All searches use the account's short name: legal suffixes like "Inc." and "LLC" and anything in parentheses are stripped. Email also matches the website domain.

- **Slack**: last `signalWindowDays`, bots excluded, Slack markup cleaned.
- **Email**: calendar-invite threads (Invitation/Accepted/Canceled…) are dropped because the calendar section covers them.
- **Calendar**: an event is kept only if its title, description or attendee emails contain the short name or domain. External attendees are anyone outside the viewer's own email domain.

## How each section is computed

| Section | Rule |
|---|---|
| Ledger: Open pipeline | Sum of `Amount` on open opps |
| Ledger: Won · 12 mo | Closed-won opps with `Amount > 0` closed in `closedLookbackDays` |
| Ledger: Next renewal | Earliest open opp whose `Type` or `Name` matches `renewalTypePattern` |
| Ledger: Executive bench | Contacts whose `Title` matches `execTitlePattern`; "engaged" means `LastActivityDate` in window |
| Ledger: Last touch | Newest timestamp across tasks, past events, email, Slack, past meetings |
| Engagement heat | 26 weekly bars counting the same touchpoints; colour runs glacier → brass → ember by intensity; header shows the 30-day change against the prior 30 days |
| Warming | New pipeline, stage advances (numbered stages only), recent wins, engagement up ≥20%, new execs or new faces, upcoming meetings, net deal-size growth |
| Cooling | Close dates slipping (history or `PushCount ≥ 2`), deals quiet more than `staleDealDays`, past-due close dates, recent losses, engagement down ≥20%, a renewal inside `renewalWatchDays` with no activity for 30 days, open escalations, zero engaged execs, net deal-size shrink |
| Deals in motion | Top 8 open by amount; stage track uses the leading stage number, or `Probability` if stages aren't numbered |
| Who's moving | New faces, title changes (cosmetic rewrites ignored), executive bench sorted by recency |
| What the team is saying | Slack and email merged, newest first, 8 items |
| On the calendar | Up to 4 upcoming meetings, then the most recent past ones |

Signals are capped at 6 per side and ordered by dollar weight or severity.

## Synthesis contract

`askClaude(SYNTH_PROMPT, [facts])` gets a compact facts object: account, ledger, computed signals, top deals, wins, people, cases, plus up to 12 Slack messages, 10 emails and 8 meetings. It must return:

```json
{"temperature":"warming|steady|cooling","bottomLine":"…","whyItMatters":[{"title":"…","body":"…"}],"warming":[{"title":"…","body":"…","source":"Slack|Email|Calendar"}],"cooling":[…],"moves":[{"title":"…","body":"…"}],"questions":["…"]}
```

If the call fails, times out (45 s) or returns invalid JSON, every section falls back to deterministic copy built from the same numbers. The page never shows an empty section.
