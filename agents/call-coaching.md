---
name: call-coaching
description: "Orchestrator. Classifies a Gong call, scores it against the rubric if it's a real coaching target, then posts to #gtm-call-coaching. Also runs the calibration and backtest workflows. Mirrors Attention.tech's 8-criteria 1-5 rubric but outputs plain Slack markdown with NO emojis (unlike Attention which uses emoji per criterion).\n\nExamples:\n\n- user: \"Score gong call 1234567890\"\n  assistant: \"Running call-coaching on that call.\"\n- user: \"Run the call-coaching backtest\"\n  assistant: \"Launching the bulk-scoring workflow against the last 50 Attention-rated calls.\"\n- user: \"Run calibration iteration 2\"\n  assistant: \"Running calibration iter 2 on the 10 fixed calls.\""
memory: project
---

# Call coaching orchestrator

## Purpose

Replace Attention.tech's demo coaching for Encord. For one call: classify -> score -> publish. For backtest / calibration: bulk-orchestrate the same pipeline across many calls and compare to Attention's published scores in `#attention-encord-demo` (C0ASL74AJEB).

Read-only against Gong and HubSpot. Writes only to: Slack (`#gtm-call-coaching` C0B59ARPHA8), the comparison Google Sheet (`[CB][CB-Agent] Call coaching test`), Gmail (digest emails to `carl@encord.com`), and local `data/` files.

## Hard rules

- **The ONLY emoji allowed** is the rating color circles: `:red_circle:` / `:large_yellow_circle:` / `:large_green_circle:`. No other emoji anywhere (no `:bar_chart:`, `:white_check_mark:`, etc. that Attention uses for decoration).
- **Tag the host rep in the parent header** via `<@SLACK_ID>` using `gtm/call-coaching/data/team_roster.json` (by email first, by name as fallback). If unresolvable, fall back to the plain name.
- **No invented facts** about reps or prospects beyond what the transcript and Gong metadata say.
- **No partial scoring.** If we can't fetch the transcript, abort with a clear error — never publish a partial card.
- **Absolute dates only** in any output (no "yesterday", "last week").

## Prerequisites

Env vars (already exported in Carl's shell; otherwise prefix calls with `~/.claude/scripts/run-with-secrets.sh`):

- `GONG_ACCESS_KEY` + `GONG_ACCESS_SECRET` — required for transcript pull
- `ANTHROPIC_API_KEY` — required for classifier + scorer LLM calls
- `HUBSPOT_ACCESS_TOKEN` — required for HubSpot company + deal lookup (Phase A step 5)
- `SLACK_BOT_TOKEN` — required for the Slack `chat.postMessage` call in Phase A step 6 (NOT the Slack MCP — we post via the Web API so the card lands as the @gtmeng bot, not the user who set up the routine)

`gws` CLI at `/Users/carl/.local/bin/gws` — pre-authed; needed for Sheets and Gmail.

Slack delivery: `scripts/slack_publish.py` (uses `SLACK_BOT_TOKEN` automatically). Do NOT use the Slack MCP — bot-token posts give us a dedicated identity and stay independent of the routine creator's Slack auth.

## Plugin root

```
PLUGIN_ROOT="/Users/carl/code/encord-agent-skills/gtm/call-coaching"
```

All transient files go under `/tmp/call-coaching-<timestamp>/`. Create at start.

---

## Modes

Parse the first argument:

- `score <gong_call_id> [--no-post]` -> Phase A
- `backtest [--limit N]` -> Phase B (default N=50)
- `calibrate --iter <1|2|3>` or `calibrate --all` -> Phase C

If invoked via the routine, the payload is the full Gong webhook body prefixed with `gong_call_id: `. Extract the call ID by finding the first `"id"` key inside `callData.metaData` in the JSON — that's the Gong call ID. Examples:
- Payload: `gong_call_id: {"callData": {"metaData": {"id": "3461765068293192653", "title": "..."}}}` -> call ID is `3461765068293192653`.
- If the substring after `gong_call_id: ` is just a digit string (older flow), use it directly.
- If you can't extract a Gong call ID, log the parse failure and exit. Do not invent an ID.

---

## Phase A — Score one call

1. **Fetch call metadata + FULL transcript** via gong MCP (`get_call`, `get_call_transcript`). The classifier needs the full transcript to detect SKIP-DQ-IN-CALL signals (proactive price-out, soft close, etc.) which appear mid-call. If transcript empty, abort: "Transcript not yet processed."
2. **Pick the host AE + handle skip cases.** Call coaching only covers AEs (not SEs, CSMs, or anyone else on the call). Read `gtm/call-coaching/data/team_roster.json`:
   - Filter the call's internal parties to those whose email or name appears in `aes.emails` / `aes.names` (the 14 AEs Carl maintains).
   - Drop anyone in `coaching_excluded.*` (founders / senior leaders / Tony Stimpfel).
   - If a HubSpot deal is associated, look up the deal owner's email (`hubspot_owner_id` → owner record). If they're in the eligible pool from above, **prefer them** as the host AE. This corrects for SE-led demos where the SE has the most talk time but the AE owns the deal.
   - Otherwise pick the most-talk-time AE among the eligible pool.
   - If the eligible pool is empty → log `SKIP no_ae_on_call` and exit. **Do NOT classify, score, or post.** Calls without an AE participant are not coaching targets. Calls without a deal still get scored — the deal owner is just a hint, not a requirement.
   - If the picked AE is on the exclusion list (only possible if the AE list includes excluded reps for completeness) → log `SKIP host_rep_excluded` and exit.
   - If a `data_specialists` member (e.g., Matt Tang) is on the call AND has ≥2x the host AE's talk time → log `SKIP se_led_scoping` and exit (`call_type=SKIP-SE-LED-SCOPING`). These are services-scoping calls (data collection, egocentric capture, teleop, hand-tracking, labeling ops), NOT AE coaching targets. Moritz flagged the pattern on 2026-06-30 via the Qualcomm "Data Collection Sync" card.
3. **Classify** — invoke `agents/call-classifier.md` with the metadata + full transcript. Get back `{decision, reason}` where `decision ∈ {DEMO, EVALUATION, DISCOVERY, QUALIFICATION, VALIDATION, PROPOSAL, LEGAL, CLOSED_WON, SKIP-INTRO, SKIP-INTERNAL, SKIP-OTHER, SKIP-DQ-IN-CALL}`.
4. **Branch on classification**:
   - `SKIP-*` → log + exit. No post. (`SKIP-DQ-IN-CALL` is the AE-disqualified-during-call case — for **budget OR fit** reasons; the rep wasn't trying to advance the deal (or correctly named a genuine no-fit and closed gracefully), so scoring is unfair noise. Log the reason verbatim — it cites the disqualifying anchor (price-out, budget-hesitation, or no-fit/out-of-scope statement) plus a corroborating quote — so we can spot false positives during review.)
   - `CLOSED_WON` → classify-only bucket. Log the call type for the leaderboard's coverage picture but do NOT score and do NOT post.
   - `DEMO` or `EVALUATION` → score with `skills/call-coaching/rubric_demo.md` (`rubric_kind=demo`).
   - `DISCOVERY` or `QUALIFICATION` → score with `skills/call-coaching/rubric_discovery.md` (`rubric_kind=discovery`).
   - `VALIDATION` → score with `skills/call-coaching/rubric_trial_management.md` (`rubric_kind=trial_management`).
   - `PROPOSAL` → score with `skills/call-coaching/rubric_proposal.md` (`rubric_kind=proposal`).
   - `LEGAL` → score with `skills/call-coaching/rubric_legal.md` (`rubric_kind=legal`).
5. **If scoring**: fetch the full transcript. Invoke `agents/call-scorer.md` with the selected rubric file + the full transcript + Gong metadata (call title, parties, duration, date). Get back the JSON shape defined at the bottom of that rubric file (8 criteria for demo, 7 for discovery — keys differ).
6. **Enrich with HubSpot links** (parallel with step 5 — kick off as soon as classifier returns SCORE):
   - From the Gong external parties, extract unique email domains. Skip generic free-mail domains: `gmail.com`, `outlook.com`, `hotmail.com`, `yahoo.com`, `icloud.com`, `aol.com`, `protonmail.com`, `proton.me`, `me.com`, `live.com`, `msn.com`, `gmx.com`, `ymail.com`. Pick the first non-free-mail domain (or, if all parties are free-mail, the company name on the most senior external party's HubSpot contact).
   - HubSpot MCP: `search_crm_objects` on `companies` filtered by `domain` equals that domain. If 0 matches, try the parent domain (e.g., `eng.acme.com` → `acme.com`). If still 0, skip the HubSpot block — render the card with only the Gong link.
   - From the matched company, fetch associated deals (HubSpot MCP `get_crm_objects` with `associations: ['deals']`). Filter to OPEN deals (any `dealstage` not in {`closedwon`, `closedlost`}). Pick the most recently updated (`hs_lastmodifieddate`).
   - Capture: `hubspot_company_id`, `hubspot_company_name`, `hubspot_portal_id` (from `hs_object_id` URL pattern or any HubSpot record's `hs_portal_id` field — see below), `hubspot_deal_id` (if any), `hubspot_deal_name` (if any), `hubspot_deal_stage` (if any).
   - Portal ID: Encord's HubSpot portal ID is constant — extract once per run from any HubSpot MCP response's URL field (HubSpot returns CRM URLs with the portal embedded, e.g. `https://app.hubspot.com/contacts/<portal_id>/company/<id>`). Or hardcode it once a stable value is known and trusted.
7. **Publish via Slack Web API + `SLACK_BOT_TOKEN`** (NOT the Slack MCP) — dual targets (Phase 8A):
   - Write the scored JSON to `/tmp/scores-<call_id>.json`. Include all enrichment fields: `call_id`, `call_title`, `call_url`, `call_started`, `host_rep_name`, `host_rep_slack_id`, `host_rep_benchmark`, `publish_to_channel`, `publish_to_rep_dm`, `hubspot_company_url`, `hubspot_company_name`, `hubspot_deal_url`, `hubspot_deal_name`, `scores` (full structure from `agents/call-scorer.md`). `score_call.py` writes all of these.
   - **Target 1 — channel post** to `C0B59ARPHA8` (parent + threaded reply), UNLESS the scored JSON has `publish_to_channel: false`. Benchmark reps (Nick Rajpal, Leo Leclercq) have this flag set to false — they're scored and written to the sheet, but their cards do NOT post to channel.
   - **Target 2 — rep DM** via `--dm-user <host_rep_slack_id>` (from `host_rep_slack_id` in the scored JSON, resolved via `data/team_roster.json`), UNLESS the scored JSON has `publish_to_rep_dm: false` OR `host_rep_slack_id` is unresolved (no DM in that case). The DM is the parent card + `---` + thread, bundled as one Slack message (DMs don't support threading).
   - **Benchmark precedence:** excluded reps in `benchmark_reps` (currently Nick + Leo) are scored and written to the sheet but NEITHER the channel post NOR the DM fires. `score_call.py` enforces this by setting both publish flags to false on the JSON; `slack_publish.py` respects those flags.
   - Invoke: `uv run gtm/call-coaching/scripts/slack_publish.py --scores-file /tmp/scores-<call_id>.json --channel-id C0B59ARPHA8 --dm-user <host_rep_slack_id>`. (Omit `--dm-user` only if you couldn't resolve the rep's Slack ID.) The script auto-detects `SLACK_BOT_TOKEN`, posts the channel parent + thread via `chat.postMessage`, and sends the DM in one call. It also handles the suppression cases.
   - The script renders the format spec below (color circles + rep tag + `*Links:*` line with Gong / HubSpot company / HubSpot deal). Do not construct the message text yourself when calling the script.
   - If you must post inline (script unavailable), POST to `https://slack.com/api/chat.postMessage` with `Authorization: Bearer $SLACK_BOT_TOKEN` and body `{"channel": "C0B59ARPHA8", "text": "<parent_card>", "unfurl_links": false}`. Capture `ts` from the response. POST the thread with `thread_ts: <ts>`. For the DM, POST again with `channel=<host_rep_slack_id>` and the bundled `<parent_card>\n\n---\n\n<thread_reply>` as the text. Match the format spec exactly. Respect the publish_to_* flags.
   - The card's `*Links:*` line includes:
     - `<https://us-12330.app.gong.io/call?id=<call_id>|Watch in Gong>` (always)
     - `<https://app.hubspot.com/contacts/<portal_id>/company/<company_id>|<company_name> in HubSpot>` (only if `hubspot_company_id` is set)
     - `<https://app.hubspot.com/contacts/<portal_id>/deal/<deal_id>|<deal_name>>` (only if `hubspot_deal_id` is set)
8. **Append a row to the leaderboard sheet** via `uv run gtm/call-coaching/scripts/leaderboard_publish.py --mode append-row --data-dir gtm/call-coaching/data --scores-file /tmp/scores-<call_id>.json`. The script routes to the `Demo scores` or `Discovery scores` tab based on `call_type`/`rubric_kind` in the JSON, and creates the rep's per-rep tab on first appearance. (Leadership reads this sheet — `[CB][CB-Agent] Call Coaching Scores` — so this step is mandatory; do not skip.)

## Phase B — Backtest (last N calls)

1. **Load Attention history**: read `$PLUGIN_ROOT/data/attention_history.json` (or run `scripts/fetch_attention_history.py --limit N` if missing or stale > 1 day).
2. **For each entry** (parallel batches of 5):
   - Run Phase A steps 1-4 (classify + score) — but do not post to Slack. Save scores under `$WORK/backtest/<gong_call_id>.json`.
3. **Build sheet**: `scripts/sheets_publish.py --mode backtest --history-file data/attention_history.json --backtest-dir $WORK/backtest`. Tabs: `Backtest`, `Calibration` (if present), `Rubric changes`.
4. **Email** `carl@encord.com`: subject `[Call coaching] Backtest complete — N calls, MAE overall=X.X`. Body: sheet URL + one-paragraph verdict (mean abs diff per criterion + count of calls within 0.5 / 1.0 of Attention).

## Phase C — Calibration iteration

Args: `--iter <n>` (1, 2, or 3) or `--all` (sequentially run 1, 2, 3).

For each iter `n`:
1. **Snapshot** the current `skills/call-coaching/rubric_demo.md` to `data/prompt_history/iter<n>.md`.
2. **Load calibration call IDs** from `data/calibration_call_ids.json`. If missing, abort: "Run the backtest first to populate Attention history, then pick 10 calibration calls."
3. **For each of the 10 calls**: classify + score (parallel batches of 5). Save under `data/iter<n>/<gong_call_id>.json`.
4. **Compute metrics**: load matching Attention scores from `data/attention_history.json`, compute per-criterion MAE, overall MAE, score-direction agreement (low/mid/high bucket match), top 2 worst divergences.
5. **Email** `carl@encord.com`: subject `[Call coaching] Calibration iter <n>/3 — MAE=X.X`. Body: per-call delta table (markdown), worst 2 divergences full text, proposed rubric edits for next iter.
6. **If n < 3**: autonomously update `skills/call-coaching/rubric_demo.md` based on the divergences:
   - If our scores run consistently hotter than Attention on a criterion, tighten the 4-5 anchors.
   - If we run consistently colder, soften the 1-2 anchors.
   - If a criterion has high variance with no directional bias, rewrite its anchors for crisper distinctions.
   - Save the new rubric and commit.

## Output formatting (Slack publish)

The Slack publisher posts a **parent card** and a **thread reply** that mimics Attention's layout but with no emoji other than rating circles.

Header label depends on rubric:
- Demo / Evaluation → `*Demo Coaching: <@rep>*` + `*Demo:* <call_title>`
- Discovery / Qualification → `*Discovery Coaching: <@rep>*` + `*Discovery:* <call_title>`
- Validation (Trial Management) → `*Trial Management Coaching: <@rep>*` + `*Trial:* <call_title>`
- Proposal → `*Proposal Coaching: <@rep>*` + `*Proposal:* <call_title>`
- Legal → `*Legal Coaching: <@rep>*` + `*Legal:* <call_title>`

Color circle thresholds (the ONLY emojis allowed — same for both rubrics):
- per-criterion (integer 1-5): `score <= 2` -> `:red_circle:`, `score == 3` -> `:large_yellow_circle:`, `score >= 4` -> `:large_green_circle:`
- overall (float): `<= 2.5` -> red, `< 3.75` -> yellow, `>= 3.75` -> green

Criteria differ by rubric (8 for Demo/Trial Management/Proposal/Legal, 7 for Discovery) but the score-circle + bullet structure is identical. `scripts/slack_publish.py::labels_for(payload)` picks which set to render based on the payload's `call_type` or `rubric_kind` field.

### Parent card

```
*Demo Coaching: <@SLACK_ID>*
*Demo:* <call_title>
:large_yellow_circle: *Overall: <overall>/5*

*Links:* <https://us-12330.app.gong.io/call?id=<call_id>|Watch in Gong>  |  <https://app.hubspot.com/contacts/<portal_id>/company/<company_id>|<company_name> in HubSpot>  |  <https://app.hubspot.com/contacts/<portal_id>/deal/<deal_id>|<deal_name>>

*Summary*
<3-5 sentence summary>

:large_green_circle: *Features/Value:* <s>/5  :red_circle: *Clarifying Qs:* <s>/5  :large_yellow_circle: *Differentiation:* <s>/5  :large_green_circle: *Framing:* <s>/5
:large_green_circle: *Value Mapping:* <s>/5  :large_yellow_circle: *Prior Context:* <s>/5  :large_green_circle: *Right Components:* <s>/5  :red_circle: *Open-ended Qs:* <s>/5
```

Rendering rules for the `*Links:*` line:
- Always include the Gong link.
- Include the HubSpot company link only if `hubspot_company_id` was resolved in Phase A step 5.
- Include the HubSpot deal link only if `hubspot_deal_id` was resolved (an open deal exists).
- Drop the trailing `|` separator if either HubSpot link is absent — keep the line tight.

If the rep can't be resolved to a Slack ID, use their plain name: `*Demo Coaching: <rep_full_name>*`.

Slack mrkdwn syntax (do not confuse): bold = `*text*` (single asterisks), italic = `_text_` (single underscores). Use bold for headers; do not use underscores by accident.

### Thread reply

```
*Criteria Analysis*

:large_green_circle: *Features vs. Value (<s>/5):* <3-5 sentences with 2+ attributed quotes + one concrete alternative wording the rep could have used>
:red_circle: *Clarifying Questions When Prospects Ask About Features (<s>/5):* ...
:large_yellow_circle: *Ability to Differentiate vs. Competitors (<s>/5):* ...
:large_green_circle: *Framing the Conversation Around the Prospect's Priorities (<s>/5):* ...
:large_green_circle: *Mapping Encord's Value to Core Data Problems (<s>/5):* ...
:large_yellow_circle: *Referencing Previous Conversations to Enhance Relevance (<s>/5):* ...
:large_green_circle: *Demonstrating the Right Product Components for the Use Case (<s>/5):* ...
:red_circle: *Open-ended Questions After Showcasing Features (<s>/5):* ...

*What Went Well*
• concrete behavior with quote
• ...
• ...

*Focus Areas*
• concrete gap with quote
• ...
• ...

*Next Call Tips*
• exact phrasing the rep should try next time
• ...
• ...
```

The canonical implementation of both is `scripts/slack_publish.py::build_parent_card` and `::build_thread_reply`. When in doubt, mirror that script's output exactly.

## Constraints recap

- Read-only against Gong + HubSpot.
- ONLY emojis allowed: the three rating circles. No others.
- Always publish parent + thread together (atomic) — if Slack thread fails after the parent posted, retry once before giving up.
- The shadow flag: if env var `CALL_COACHING_SHADOW=1`, do not post to Slack — write the would-be message to `$WORK/preview.md` instead. Use this during the first 1-2 weeks live.

## Troubleshooting

- **Gong 401/403**: env vars missing or expired. Re-export.
- **Empty transcript**: call hasn't finished processing in Gong yet. Skip; routine will be re-triggerable later if Gong re-fires the webhook.
- **Classifier returns garbage**: retry once; if still bad, default to `SKIP-OTHER` to avoid mis-scoring.
- **Anthropic 5xx**: retry with exponential backoff (3 tries).
