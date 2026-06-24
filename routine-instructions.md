# GCP Migration Dashboard — Routine Instructions

## What this routine does
Checks Slack for updates, determines what changed since the last run, updates the dashboard HTML, pushes to GitHub Pages, and drops a Slack draft in Wajih's DM for review before it goes to the team.

## Files
- Dashboard HTML: `/Users/wajihbizreh/Downloads/gcp-migration-dashboard.html`
- Git repo: `/tmp/gcp-dashboard/`
- GitHub Pages: https://wajihgc.github.io/gcp-migration-dashboard/
- Push command: `git push https://WajihGC:$(gh auth token --hostname github.com)@github.com/WajihGC/gcp-migration-dashboard.git HEAD:main`

## Slack channels to check (search last 3 days)
- `#stack-2-and-gcp-planning` (C089ECK4J73) — MySQL, Engine, Core Resilience
- `#ext-geocomply-zencore` (C08J4PNJZ2N) — GeoGuard, CMS/GCI, Security, S3→GCS
- `#engine-costs-2026` — MySQL cost analysis, Kirill's research
- `#engine-cicd-containerization` — Engine containerization progress
- Wajih's DM (U057V3QCLK0) — check for any self-notes Wajih has left

## Search queries to run
1. `from:kirill.polishchuk` — MySQL PoC progress
2. `GeoGuard Phase zencore` — GeoGuard Phase 1/2 status
3. `Valkey CMS GCI S3 GCS cutover` — CMS/GCI migration status
4. `Databricks contract MBR` — Databricks updates
5. `MongoDB credit AWS Andrii` — MongoDB credit status
6. `Engine V1 GCP containerization Jun 30` — Engine deadline
7. `Core Resilience Security NGFW` — Security workstream

## Sections to update
Only update a section when Slack confirms something materially changed. Never update without a source. Do not remove existing content without a source confirming it changed.

### Workstream order (do not reorder)
1. Core / Engine & MySQL
2. Core Resilience & Security
3. ML Migration & Databricks
4. GeoGuard & CMS / GCI
5. Financial Health

## Voice and formatting rules
- Short declarative sentences. Status first, then detail.
- No em dashes. No filler ("Additionally", "Furthermore", "It's worth noting").
- No pleasantries.
- Bold key dates, statuses, and owner names.
- If something is blocked, say blocked. If at risk, say at risk.
- Direct, peer-level tone — no teaching, no hedging.

## Flagging rules
Assert as fact only when confirmed in Slack or a Jira ticket.
If you cannot find a source:
- Flag it in your session report to Wajih
- Do not include the unconfirmed claim in the dashboard
- Do not silently leave old content in place if you know it's wrong — flag the conflict

## Standing items — always verify, update if changed
| Item | Current status | Watch for |
|---|---|---|
| Engine V1 GCP | Jun 30 deadline, AT RISK | Completion confirmation or slip announcement |
| Engine V1 Prod | Jul 31 deadline | Dependency on Jun 30 |
| Core Resilience | Jul 31 target, BLOCKED | Engine team response to Kirill's MySQL analysis |
| MySQL PoC | 2 paths: MySQL replication (0.5–1% collision) vs. single primary write (zero collision). Engine team input (Hieu, Artem, Thomas) pending | Engine team response, Steven Vo decision |
| MySQL DR Topology | Blocked — awaiting Engine team then Steven Vo | Decision announcement |
| CMS/GCI S3→GCS | Scheduled Jun 24 — check if completed | Completion message in #ext-geocomply-zencore |
| GeoGuard Phase 1 | Underway (ZenCore). Phase 2 blocked on Ph1 | Phase 1 completion confirmation |
| GeoGuard MP/GCP integration | Still in discussions, no alignment | Any alignment announcement |
| Databricks | Contract in review. MBR Jul 7 3PM ET | Contract decision, MBR outcome |
| MongoDB $500K AWS credit | Aug 31 hard deadline, no extension | Confirmation Andrii submitted |
| Security / NGFW | Evaluation ongoing, no tech selection | Selection announcement |

## Highlight cards to keep current
- Overall status badge (At Risk / On Track / Blocked)
- Open Decisions count and blurb (currently 2, waiting on Steven Vo)
- Nearest deadline

## After updating the dashboard
1. `cp /Users/wajihbizreh/Downloads/gcp-migration-dashboard.html /tmp/gcp-dashboard/index.html`
2. `cd /tmp/gcp-dashboard && git add index.html`
3. `git commit -m "update: <date> routine refresh — <one line summary>"`
4. Push with HTTPS token (see push command above)
5. Create Slack draft in Wajih's DM (U057V3QCLK0) using `slack_send_message_draft`

## Draft message template
```
Hi team — GCP Migration Dashboard updated for <date>.

<status_emoji> **Overall: <status>** · Nearest deadline: <deadline> · <N> days

**Key updates:**
- [only items that materially changed since last draft]

:point_right: Dashboard: https://wajihgc.github.io/gcp-migration-dashboard/

FYI @Steven Vo @Nataliia Kyrychenko
```
Only list items in Key Updates that actually changed. If nothing changed in a workstream, do not mention it.

## Session report to Wajih (always end with this)
After dropping the draft, report:
1. What changed and the Slack source
2. Anything flagged (claimed in dashboard but no source found)
3. Anything that needs Wajih's input before sending

## How to handle feedback from Wajih in this session
1. Apply the correction to the dashboard and push
2. Update the draft in Wajih's DM
3. Propose the exact addition to the Corrections Log below (do not auto-write — wait for Wajih to confirm)

## Corrections log
- [2026-06-22] Never say "Hieu and Rost have options prepared" without checking Kirill's latest research — his analysis supersedes the older DR options framing
- [2026-06-22] GeoGuard Phase 1: never mark complete without explicit ZenCore confirmation in #ext-geocomply-zencore
- [2026-06-22] MongoDB credit: "Andrii is submitting" has no Slack paper trail — flag until confirmed
- [2026-06-24] MySQL PoC: cron-every-30s ruled out (Kibana data Jun 22). Two paths: MySQL replication vs. single primary write. Engine team input needed before Steven Vo decides.
