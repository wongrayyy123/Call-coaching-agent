# Trial Management Rubric (v1 — Validation / Trial Management scorecard from Leo's gsheet)

Score each criterion 1-5 using the anchors below. Overall = arithmetic mean of the 8 scores, rounded to two decimals.

Source: [Leo's Validation / Trial Management scorecard tab](https://docs.google.com/spreadsheets/d/1ByqU5GE6L0_nL0gtmFXtJxsgHs8mkN1N-t1-3MWC4Js/edit).

Apply this rubric to **Validation** calls — active POC / trial check-ins, blocker triage, trial progress reviews. NOT post-contract account syncs (those are CLOSED_WON and not scored). The scorer must read this file before scoring any Validation call. Output the canonical JSON shape at the bottom — the keys are stable across rubric revisions.

---

## 1. Re-anchoring on the "Why" Behind the Trial

**Question:** How effectively did the rep open the call by recapping the pain, the business case, and the specific reason the trial/POC is happening, rather than treating it as a generic check-in?

- **1** — The rep opened with a generic check-in ("how's the trial going?") and never referenced the original pain, the business outcome at stake, or why the trial was agreed. The call had no anchor.
- **2** — The rep made a passing reference to the trial but did not connect it to the prospect's pain or the business reason for evaluating Encord. Mostly logistics.
- **3** — The rep loosely recapped what the trial is testing but did not tie it back to the business outcome or original pain in a way that created focus or urgency.
- **4** — The rep recapped the pain and the purpose of the trial and connected it to a business outcome, but the framing was brief or not used to steer the rest of the call.
- **5** — The rep explicitly re-anchored the call on the original pain, the business outcome at stake, and the agreed reason for the trial — e.g. 'we're running this POC to prove we can cut your QA cycle from 3 weeks to under 1, which unlocks your Q3 model launch' — and used that frame to drive the agenda.

**Answer guide:** Assess whether the rep treated the trial as a purposeful test tied to a business outcome rather than a hopeful check-in. The playbook is explicit that the AE must 're-cap why we are doing the trial, not just hope we are doing the trial.' Rate 5 if the rep, early in the call, restated the prospect's core pain, the measurable business outcome the trial is meant to prove, and the agreed success criteria, then used that to focus the conversation. Look for phrases like 'the reason we kicked this off was...', 'what we're trying to prove here is...', 'if we hit X, you said that unlocks Y for the business.' Rate 4 if the recap is present but brief or not used to steer the call. Rate 3 if the rep references what's being tested but omits the business why. Rate 2 if there's only a passing logistical mention. Rate 1 if the call opens as a generic status check with no anchor to pain or value. Bad examples: 'just wanted to see how it's going' with no framing; jumping straight into feature troubleshooting without restating purpose.

## 2. Customer-Defined Success Criteria & Mutual Success Plan

**Question:** How effectively did the rep establish, reinforce, or hold the prospect to a mutual success plan with specific, customer-defined success criteria?

- **1** — No mutual success plan exists or is referenced. Success criteria are vague, undefined, or were written entirely by Encord with no customer input.
- **2** — A loose notion of success was mentioned but it is generic ('make sure it works for you') and not documented, measurable, or owned by the customer.
- **3** — Some success criteria exist but they lack specificity or clear customer ownership; the rep did not push the prospect to define what success concretely means for them.
- **4** — A documented mutual success plan with mostly specific criteria exists and the rep referenced it, but some criteria remain Encord-defined or lack measurable thresholds/owners.
- **5** — The rep worked from a documented mutual success plan with specific, measurable, customer-defined criteria and named owners/dates, explicitly getting the prospect to articulate the proof they need — e.g. 'you told us success is labeling 10k frames at 95% agreement within two weeks with two annotators trained.'

**Answer guide:** Evaluate whether validation is anchored to a customer-owned mutual success plan rather than a vague trial. The playbook stresses: 'Do not accept success criteria written by Encord as good enough, get the customer to give specificity,' and validation entry requires 'an agreed upon mutual success plan... that the customer has given input on.' Rate 5 if the rep references a documented plan with specific, measurable, customer-defined criteria and named owners, and actively gets the prospect to specify the proof they need to move forward. Look for: 'what would you need to see by the end of this to be confident?', 'let's write down exactly what success looks like,' 'who on your side owns evaluating each of these?' Rate 4 if a plan exists and is referenced but some criteria are still Encord-defined or unmeasured. Rate 3 if criteria exist but are vague or not clearly customer-owned. Rate 2 if success is mentioned only generically. Rate 1 if there is no plan or criteria. Bad examples: accepting 'we'll just play around with it' as scope; success criteria authored solely by the rep with no customer confirmation.

## 3. Driving & Monitoring Platform Usage

**Question:** How effectively did the rep monitor actual usage of the platform during the trial and drive adoption across the prospect's team?

- **1** — The rep showed no awareness of whether the prospect is actually using the platform and did nothing to drive usage. (A trial with no usage is a major red flag in the playbook.)
- **2** — The rep asked generically whether they'd 'had a chance to log in' but did not check real usage or address low/no adoption.
- **3** — The rep referenced usage at a surface level but did not dig into who is using it, what they've done, or where adoption has stalled.
- **4** — The rep referenced specific usage signals and addressed adoption gaps, but did not fully drive a plan to increase usage among the right users.
- **5** — The rep came prepared with specific usage data (who logged in, what was annotated/curated, where activity dropped off), proactively addressed low-usage areas, and drove a concrete plan to activate the right users — treating usage as the leading indicator of validation.

**Answer guide:** Assess whether the rep treats in-tool usage as the core signal of a healthy trial. The playbook lists 'Check on usage' as a best practice and flags 'kick off the trial and there is no usage in the tool' as a red flag. Rate 5 if the rep references concrete usage signals (logins, frames labeled, projects created, Index/Active activity), proactively surfaces and troubleshoots low-usage areas, and drives a specific plan to activate the right users. Look for: 'I noticed two of your annotators haven't logged in yet — what's blocking them?', 'you've labeled 2k frames; let's get the next batch loaded.' Rate 4 if usage is referenced specifically and gaps addressed but no clear activation plan is set. Rate 3 if usage is mentioned only at a surface level. Rate 2 if the rep asks generically without real data. Rate 1 if usage is not tracked or addressed at all. Bad examples: never mentioning whether anyone is in the platform; accepting 'we've been busy' without re-driving usage.

## 4. Decision-Maker & Stakeholder Engagement

**Question:** How effectively did the rep keep an economic decision-maker engaged during validation and avoid single-threading?

- **1** — The rep is engaging only a single technical user; no decision-maker is involved and there's no plan to involve one. The 'evaluation team will hand results to leadership' dynamic is accepted.
- **2** — A decision-maker has been mentioned but the rep has no access and made no attempt to engage them during the trial.
- **3** — The rep acknowledged the need to involve a decision-maker or additional stakeholders but did not take concrete steps during the call to do so.
- **4** — The rep is multi-threaded and has some decision-maker engagement, but key stakeholders remain unconfirmed or under-engaged in the validation.
- **5** — The rep has the economic decision-maker actively engaged in the validation (or secured a concrete commitment to engage them), is multi-threaded across the relevant buying group, and is using the trial to build consensus rather than relying on a hand-off.

**Answer guide:** Evaluate whether the deal is multi-threaded and whether someone who can decide is genuinely involved, as the playbook requires for validation entry ('someone who can make a decision is involved at this point') and warns against ('no engagement with DM,' 'evaluation team will hand off the results... to leadership'). The training reinforced that a technical validation with the wrong person can be wasted if a skeptical economic buyer later blocks it. Rate 5 if a decision-maker is actively engaged (or a firm commitment to engage them is secured) and the rep is multi-threaded. Look for: 'who else needs to weigh in on the results?', 'let's get [VP] on the readout call,' asking about additional users/stakeholders. Rate 4 if multi-threaded but some key stakeholders are under-engaged. Rate 3 if the need is acknowledged but not acted on. Rate 2 if a DM is known but untouched. Rate 1 if single-threaded with a hand-off dynamic accepted. Bad examples: running the entire POC with one ML engineer and assuming they'll sell it upward; never asking who signs off.

## 5. Executive Alignment Before Deploying Resources

**Question:** How effectively did the rep secure executive alignment before committing customisation, FDE, or significant technical resources to the validation?

- **1** — The rep committed (or offered to commit) FDE/customisation/significant technical resource with no executive alignment and no qualification of whether it's warranted.
- **2** — The rep discussed deploying resources but did not connect it to executive buy-in or the deal's value/size.
- **3** — The rep is aware alignment is needed before deploying resources but has not secured it, or proceeded without confirming it.
- **4** — The rep secured some alignment before resourcing but it is informal or not tied to a clear commitment from the customer's side.
- **5** — The rep explicitly secured executive alignment (on both sides where relevant) before committing customisation/FDE/technical resource, tying the investment to the deal's value and a reciprocal customer commitment — protecting Encord's limited resources.

**Answer guide:** Assess whether scarce technical resources are deployed only with executive alignment, per the playbook: 'if there is any customisation, FDE, technical resource to be deployed, there must be executive alignment prior to doing so.' The training emphasised that SEs/FDEs are genuinely constrained and that friction/qualification should precede resource investment. Rate 5 if the rep secured executive alignment before any meaningful resource commitment and tied it to a reciprocal customer commitment. Look for: 'before we put an FDE on this, I want to make sure your leadership is bought into the outcome,' 'let's confirm exec sponsorship before we build the custom workflow.' Rate 4 if alignment is secured but informal. Rate 3 if the need is recognised but unmet. Rate 2 if resources are discussed without tying to alignment. Rate 1 if resources are offered freely with no alignment or qualification. Bad examples: promising a custom integration to a junior user to keep a trial alive; deploying FDE time before any decision-maker has committed.

## 6. Surfacing & Resolving Blockers; Communication Cadence

**Question:** How effectively did the rep surface technical/operational blockers and maintain frequent, proactive communication throughout the trial?

- **1** — The rep neither surfaced nor resolved blockers and there is no evident communication cadence; the trial is drifting.
- **2** — Blockers were mentioned only when the prospect raised them, and communication is sporadic and reactive.
- **3** — The rep addressed some blockers but did not proactively dig for hidden ones, and the cadence is loosely defined.
- **4** — The rep proactively surfaced and worked most blockers and maintained a reasonable cadence, with minor gaps in follow-through or frequency.
- **5** — The rep proactively dug for blockers (technical and organisational), drove them to resolution with clear owners, and maintained a frequent, agreed cadence across calls and Slack — validating the engagement as well as the platform.

**Answer guide:** Evaluate whether the rep is actively de-risking the trial and staying close, per the playbook: 'keep communication frequent through calls/slack' and 'validation is done on both our platform as well as our engagement.' The Demo/Discovery rubrics reward digging for risks rather than settling for 'looks great.' Rate 5 if the rep proactively surfaces blockers, assigns owners, drives resolution, and sustains a frequent cadence (calls + Slack). Look for: 'what's getting in the way that we haven't talked about?', 'I'll have our SE jump on that today and confirm by Thursday,' evidence of an agreed check-in rhythm. Rate 4 if most blockers are worked and cadence is reasonable. Rate 3 if some blockers are handled but none are proactively surfaced. Rate 2 if blockers are addressed only reactively with sporadic contact. Rate 1 if the trial is drifting with no cadence. Bad examples: waiting for the prospect to report problems; going silent for a week mid-trial.

## 7. Quantifying Value & Building the Business Case

**Question:** How effectively did the rep tie trial results to measurable business outcomes and build the business case, rather than validating features in isolation?

- **1** — The conversation stayed at the feature/'it works' level with no connection to business outcomes, ROI, or quantified value.
- **2** — The rep mentioned value generically ('this should save time') without quantifying it or tying it to the prospect's metrics.
- **3** — The rep connected some trial results to outcomes but inconsistently, and did not build toward a quantified business case.
- **4** — The rep tied most trial results to business outcomes and began quantifying value, with minor gaps in rigour or customer validation of the numbers.
- **5** — The rep consistently translated trial results into the prospect's own business metrics (cost, throughput, time-to-production, quality) and co-built a quantified business case the buyer can own — turning 'it works' into 'here's what it's worth.'

**Answer guide:** Assess whether the rep is converting technical validation into a quantified business case, which the playbook defines as the objective of this stage ('the buyer must provide proof of solution and business case'). The training repeatedly stressed that without a tied business outcome, even a strong technical result loses to do-nothing/status-quo because Encord becomes 'just a tool' buying features. Rate 5 if the rep consistently maps trial outcomes to the prospect's metrics and co-builds a quantified case the buyer can articulate. Look for: 'based on the throughput we just hit, that's roughly X hours/week saved across your team,' 'what does shipping this model a month earlier mean in revenue?' Rate 4 if outcomes are tied and value is partially quantified. Rate 3 if connections are inconsistent. Rate 2 if value is only generic. Rate 1 if it stays purely at the feature level. Bad examples: ending validation with 'the team likes it' and no numbers; demonstrating capability without translating it into business impact.

## 8. Mapping the Path to Commercial Discussion & Procurement

**Question:** How effectively did the rep secure commitment to a commercial discussion and begin mapping the procurement/buying path before exiting validation?

- **1** — No discussion of next steps toward a commercial conversation; the trial has no defined off-ramp into buying.
- **2** — The rep vaguely referenced 'talking pricing later' with no commitment or process mapping.
- **3** — The rep raised the move to commercials but did not secure commitment or explore the buying/procurement process.
- **4** — The rep secured a commitment to a commercial discussion and touched on the buying process, but with gaps (e.g. procurement, signatories, or timeline not yet explored).
- **5** — The rep secured a clear commitment to a commercial discussion contingent on hitting success criteria, and began mapping the buying process — decision-makers, procurement, and rough timeline — setting up a clean exit into Proposal.

**Answer guide:** Evaluate whether the rep is converting a successful trial into forward motion, per the playbook buyer action ('outline process to move forward into procurement') and the call-type definition ('confirming the prospect is committed to entering a meaningful commercial discussion'). Rate 5 if the rep ties the move to commercials to hitting the agreed success criteria and starts mapping the buying process (decision-makers, procurement, timeline). Look for: 'if we hit these criteria, are you ready to move into commercials?', 'once we prove this out, what does your buying process look like and who's involved?' Rate 4 if commitment is secured but the buying process is only partially mapped. Rate 3 if the move is raised without commitment or process. Rate 2 if it's a vague 'later.' Rate 1 if there's no path defined. Bad examples: finishing a successful POC with no agreed next commercial step; never asking how the prospect buys software.

---

## Output JSON shape (what the scorer must produce)

```json
{
  "rubric": "trial_management",
  "overall": 3.25,
  "criteria": {
    "re_anchoring_why":            {"score": 3, "analysis": "..."},
    "mutual_success_plan":         {"score": 2, "analysis": "..."},
    "platform_usage":              {"score": 3, "analysis": "..."},
    "decision_maker_engagement":   {"score": 4, "analysis": "..."},
    "executive_alignment":         {"score": 4, "analysis": "..."},
    "surfacing_blockers":          {"score": 4, "analysis": "..."},
    "quantifying_value":           {"score": 4, "analysis": "..."},
    "path_to_commercial":          {"score": 2, "analysis": "..."}
  },
  "summary": "...",
  "what_went_well": ["..."],
  "focus_areas": ["..."],
  "next_call_tips": ["..."]
}
```

Each `analysis` is 3-5 sentences with at least 2 attributed direct quotes and one concrete alternative wording the rep could have used (per `agents/call-scorer.md`).
