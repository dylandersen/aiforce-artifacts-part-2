# CFO Revenue Ledger: data contract

Every figure is built from these queries at view time. Only small per-viewer preferences (scope, period, plan, recents) live in `localStorage`.

| Section | Query |
|---|---|
| Totals | Opportunity aggregate by ForecastCategoryName, IsClosed, IsWon for `CloseDate = <period>` |
| Losses | Opportunity aggregate with `CONFIG.lostWhere` |
| Ledger | Top 25 Opportunity by Amount, open or won, not Omitted |
| Slip risk | Open Opportunity with PushCount ≥ 2, past-due close, or LastActivityDate older than `quietDays` (60 s time-box) |
| Renewals | Open Opportunity matching `renewalWhere`, grouped by calendar month, next six months |
| Viewer | `chatter/users/me`, then User (Title, UserRole.Name, UserRole.ParentRoleId, Profile.Name) and a COUNT of direct reports; decides the default scope |
| Scope picklist | Direct reports of the viewer; User grouped by ManagerId for the org's leaders (top 25 by team size) |
| Periods | Period (Quarter, Year) for fiscal labels, bounds and days left; falls back to Organization.FiscalYearStartMonth |

## Probe calls

- Salesforce: `{url:"/services/data/v66.0/query", method:"GET", queryParams:{q:"SELECT Id, Name FROM Opportunity LIMIT 1"}}` → `{status_code, body:{records}, url}`. The `url` origin builds record links.
- Identity: `{url:"/services/data/v66.0/chatter/users/me", method:"GET"}` → `{body:{id, name}}`.


## Scope

Scope is either the company (no owner filter) or a leader plus up to three levels of reports: `OwnerId = X OR Owner.ManagerId = X OR Owner.Manager.ManagerId = X OR Owner.Manager.Manager.ManagerId = X`. Periods use `THIS_FISCAL_QUARTER`, `NEXT_FISCAL_QUARTER` and `THIS_FISCAL_YEAR`, labelled from the Period object.

## Synthesis

Where the page uses Claude, it passes a compact facts object to `askClaude` and expects minified JSON. If the call fails, times out or returns invalid JSON, the section shows copy computed from the same numbers.
