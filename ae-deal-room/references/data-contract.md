# AE Deal Room: data contract

Every figure is built from these queries at view time. Only small per-viewer preferences (scope, period, plan, recents) live in `localStorage`.

| Section | Query |
|---|---|
| Picker | Open Opportunity owned by the signed-in user; SOSL search across Opportunity names |
| Deal | Opportunity by Id with Histories, Tasks, Events and OpportunityContactRoles subqueries |
| Slack / Email / Calendar | Search by the account's short name and website domain |
| Drawer detail (on first open) | Opportunity LeadSource, Description, OpportunityCompetitors, OpportunityLineItems and full field history with who changed it; senior Contacts at the account matching `execLike`; other open Opportunities at the account |

## Probe calls

- Salesforce: `{url:"/services/data/v66.0/query", method:"GET", queryParams:{q:"SELECT Id, Name FROM Opportunity LIMIT 1"}}` → `{status_code, body:{records}, url}`. The `url` origin builds record links.
- Identity: `{url:"/services/data/v66.0/chatter/users/me", method:"GET"}` → `{body:{id, name}}`.
- Slack: `{keywords:["Acme"], limit:5, sort:"timestamp", response_format:"detailed", include_context:false}` → markdown `### Result` blocks with Channel, From, Time, Permalink, Text.
- Gmail: `{query:"\"Acme\" newer_than:90d", pageSize:5, view:"THREAD_VIEW_SUMMARY"}` → `{threads:[…]}`.
- Calendar: `{query:"Acme", pageSize:5}` → `{events:[…]}`.

## Scope

Scope is either the company (no owner filter) or a leader plus up to three levels of reports: `OwnerId = X OR Owner.ManagerId = X OR Owner.Manager.ManagerId = X OR Owner.Manager.Manager.ManagerId = X`. Periods use `THIS_FISCAL_QUARTER`, `NEXT_FISCAL_QUARTER` and `THIS_FISCAL_YEAR`, labelled from the Period object.

## Synthesis

Where the page uses Claude, it passes a compact facts object to `askClaude` and expects minified JSON. If the call fails, times out or returns invalid JSON, the section shows copy computed from the same numbers.
