# GCP Migration Dashboard — Routine Instructions

## What this routine does
Checks Slack for updates since the last run, updates the dashboard, pushes to GitHub Pages, and drops a Slack draft in Wajih's DM for review before it goes to the team.

## Dashboard file
Read the current dashboard from GitHub:
https://raw.githubusercontent.com/WajihGC/gcp-migration-dashboard/main/index.html

After making updates, write the new version back to the repo using the GitHub connector:
- Repo: WajihGC/gcp-migration-dashboard
- Branch: main
- File: index.html

GitHub Pages will serve the updated file automatically at:
https://wajihgc.github.io/gcp-migration-dashboard/

## Slack channels to check (search last 3 days)
- #stack-2-and-gcp-planning (C089ECK4J73) — MySQL, Engine, Core Resilience
- #ext-geocomply-zencore (C08J4PNJZ2N) — GeoGuard, CMS/GCI, Security, S3→GCS
- #engine-costs-2026 — MySQL cost analysis, Kirill's research
- #engine-cicd-containerization — Engine containerization progress

## Search queries to run
1. from:kirill.polishchuk — MySQL PoC progress
2. GeoGuard Phase zencore — GeoGuard Phase 1/2 status
3. Valkey CMS GCI S3 GCS cutover — CMS/GCI migration status
4. Databricks contract MBR — Databricks updates
5. MongoDB credit AWS Andrii — MongoDB credit status
6. Engine V1 GCP containerization Jun 30 — Engine deadline
7. Core Resilience Security NGFW — Security workstream

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
- Do not silently leave old content in place if you know it is wrong — flag the conflict

## Standing items — always verify, update if changed
| Item | Current status | Watch for |
|---|---|---|
| Engine V1 GCP | Jun 30 deadline, AT RISK | Completion confirmation or slip announcement |
| Engine V1 Prod | Jul 31 deadline | Dependency on Jun 30 |
| Core Resilience | Jul 31 target, BLOCKED | Engine team response to Kirill's MySQL analysis |
| MySQL PoC | 2 paths: MySQL replication (0.5-1% collision) vs. single primary write (zero collision). Engine team input (Hieu, Artem, Thomas) pending | Engine team response, Steven Vo decision |
| MySQL DR Topology | Blocked — awaiting Engine team then Steven Vo | Decision announcement |
| CMS/GCI S3 to GCS | Scheduled Jun 24 — check if completed | Completion message in #ext-geocomply-zencore |
| GeoGuard Phase 1 | Underway (ZenCore). Phase 2 blocked on Ph1 | Phase 1 completion confirmation |
| GeoGuard MP/GCP integration | Still in discussions, no alignment | Any alignment announcement |
| Databricks | Contract in review. MBR Jul 7 3PM ET | Contract decision, MBR outcome |
| MongoDB $500K AWS credit | Aug 31 hard deadline, no extension | Confirmation Andrii submitted |
| Security / NGFW | Evaluation ongoing, no tech selection | Selection announcement |

## Highlight cards to keep current
- Overall status badge (At Risk / On Track / Blocked)
- Open Decisions count and blurb (currently 2, waiting on Steven Vo)
- Nearest deadline

## Draft message template
Send a Slack draft to U057V3QCLK0 (Wajih's DM) using slack_send_message_draft:

Hi team — GCP Migration Dashboard updated for <date>.

<status_emoji> Overall: <status> · Nearest deadline: <deadline> · <N> days

Key updates:
- [only items that materially changed since last draft]

Dashboard: https://wajihgc.github.io/gcp-migration-dashboard/

FYI @Steven Vo @Nataliia Kyrychenko

Only list items that actually changed. If nothing changed in a workstream, do not mention it.

## Session report to Wajih (always end with this)
After dropping the draft, report:
1. What changed and the Slack source
2. Anything flagged (claimed in dashboard but no source found)
3. Anything that needs Wajih's input before sending

## How to handle feedback from Wajih in this session
1. Apply the correction to the dashboard and push to GitHub
2. Update the Slack draft
3. Propose the exact addition to the Corrections Log below — do not write it without Wajih confirming

## Corrections log
- [2026-06-22] Never say "Hieu and Rost have options prepared" without checking Kirill's latest research — his analysis supersedes the older DR options framing
- [2026-06-22] GeoGuard Phase 1: never mark complete without explicit ZenCore confirmation in #ext-geocomply-zencore
- [2026-06-22] MongoDB credit: "Andrii is submitting" has no Slack paper trail — flag until confirmed
- [2026-06-24] MySQL PoC: cron-every-30s ruled out (Kibana data Jun 22). Two paths: MySQL replication vs. single primary write. Engine team input needed before Steven Vo decides.
