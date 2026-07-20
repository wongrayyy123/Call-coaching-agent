# Proposal Rubric (v1 — Proposal / Pricing scorecard from Leo's gsheet)

Score each criterion 1-5 using the anchors below. Overall = arithmetic mean of the 8 scores, rounded to two decimals.

Source: [Leo's Proposal / Pricing Call scorecard tab](https://docs.google.com/spreadsheets/d/1ByqU5GE6L0_nL0gtmFXtJxsgHs8mkN1N-t1-3MWC4Js/edit).

Apply this rubric to **Proposal** calls — commercial discussions where the AE walks through pricing/packaging, negotiates terms, builds consensus, and pushes for verbal commitment. NOT trial check-ins (Validation), NOT legal/procurement workstreams (Legal). The scorer must read this file before scoring any Proposal call. Output the canonical JSON shape at the bottom — the keys are stable across rubric revisions.

---

## Scoring gate — one-shot activities (criteria 1, 2, 3)

Delivering the Proposal Live (#1), Tailoring Scope & Mapping Line Items to Value (#2), and Anchoring Price in the Business Case / ROI (#3) all describe activities that happen ONCE per deal at the initial proposal walkthrough. On a Proposal-classified follow-up call — signature push, redline handling, order-form send-off — the walkthrough is not expected to be re-run.

Before scoring #1, #2, or #3: check `prior_deal_context`. If any `prior_gong_calls[*]` / `prior_coached_calls[*]` / `hubspot_engagements.*` entry shows a prior call where the proposal walkthrough / line-item review / pricing anchor already happened (evidence: pricing walkthrough noted, line items listed, order form drafted, packaging discussed), **default to 4 on that criterion and cite the prior call in the analysis** — quote the field the reference came from. Only score 1-3 when this is the first commercial call OR the rep re-opened the proposal from scratch on this call.

This gate exists because the classifier's "PROPOSAL" bucket covers both the initial walkthrough call and later signature-push calls; the rubric anchors are written for the initial walkthrough, so a follow-up call scored naively looks like a failed proposal.

---

## 1. Delivering the Proposal Live

**Question:** Did the rep present and walk the prospect through the proposal live, rather than sending pricing over email?

- **1** — Pricing/the proposal was sent by email with no live walkthrough, or the rep proposed to 'just send it over.'
- **2** — The proposal was largely emailed; any live discussion was minimal and did not walk through the offer.
- **3** — The rep discussed the proposal live but did not control the walkthrough — the prospect was left to interpret much of it alone.
- **4** — The rep delivered the proposal live and walked through most of it, with minor lapses in control or framing.
- **5** — The rep delivered the proposal live, controlled the walkthrough end to end, framed each element intentionally, and read/responded to reactions in real time before any document was left behind.

**Answer guide:** Assess adherence to the playbook rule: 'Proposals are to be delivered live, not via email. Proposals are intentional, and not hopeful.' Delivering live lets the rep control framing, handle reactions, and avoid the proposal being shopped or misread. Rate 5 if the rep presents live, drives the walkthrough, frames each component deliberately, and gauges reactions before sending anything. Look for: 'let me walk you through this rather than just sending it,' screen-sharing the proposal, pausing for reactions per section. Rate 4 if delivered live with minor control lapses. Rate 3 if discussed live but the prospect largely self-navigates. Rate 2 if mostly emailed with token discussion. Rate 1 if emailed with no walkthrough. Bad examples: 'I'll fire the pricing over and you can review' with no call; sending a PDF and asking for thoughts async.

## 2. Tailoring Scope & Mapping Line Items to Value

**Question:** How effectively did the rep tailor the proposal's scope/packaging to the validated use case and tie every line item to specific customer value?

- **1** — A generic proposal with line items unconnected to anything the prospect validated or values; feels like a price list.
- **2** — The proposal references the prospect's use case loosely, but most line items are presented without a value rationale.
- **3** — Some line items are tied to value, but the rep drifts into listing components/prices without consistent justification.
- **4** — Most line items are mapped to validated value and the scope reflects the use case, with a few components left unjustified.
- **5** — Every line item and the overall packaging map directly to validated outcomes and the prospect's stated value — nothing is out of place — e.g. Annotate seats tied to their labeling volume, Active tied to the QA problem they validated.

**Answer guide:** Evaluate against the playbook standard: 'Every line item and word on the proposal should be able to be mapped to customer value, nothing out of place,' and 'present a clear, tailored commercial offer.' Rate 5 if scope/packaging reflect the validated use case and each line item is justified by a specific value/outcome the prospect cares about (mapping to Annotate/Active/Index/Workflows/Data Agents as relevant). Look for: 'we've scoped Annotate to your 50k-frames/month volume,' 'Active is here because of the QA rework you flagged.' Rate 4 if most items are mapped with minor gaps. Rate 3 if value-mapping is inconsistent. Rate 2 if the use case is referenced but items aren't justified. Rate 1 if it's a generic price list. Bad examples: including modules the prospect never needed; presenting seat counts or add-ons with no link to validated usage.

## 3. Anchoring Price in the Business Case / ROI

**Question:** How effectively did the rep re-establish the business case and value before presenting price, rather than leading with cost?

- **1** — The rep led with price with no value framing; the proposal stands on cost alone.
- **2** — Minimal value framing; a token reference to benefits before numbers.
- **3** — Some business-case framing precedes price but it is generic and not tied to the prospect's quantified outcomes.
- **4** — The rep re-anchored on the business case before price using mostly specific outcomes, with minor gaps in quantification.
- **5** — The rep re-anchored firmly on the quantified business case/ROI before revealing price — framing cost against the value validated in the trial — so price is evaluated relative to value, not in isolation.

**Answer guide:** Assess whether price is contextualised by value, consistent with the playbook ('align on scope, pricing, and value'; buyer should 'articulate the value and ROI of Encord') and the best practice that delivering pricing too early weakens position. The training stressed that without a business case the buyer defaults to status quo and treats Encord as 'just a tool.' Rate 5 if the rep restates the quantified business case/ROI before price and frames cost against validated value. Look for: 'before we get to numbers, let's recap what this unlocks — X hours saved, Y faster to production,' 'against that value, here's the investment.' Rate 4 if anchored with minor quantification gaps. Rate 3 if framing is generic. Rate 2 if framing is token. Rate 1 if it leads with price. Bad examples: opening the pricing call with the dollar figure; presenting price with no reference to the validated outcome.

## 4. Building Consensus & Confirming Decision-Makers/Signatories

**Question:** How effectively did the rep build consensus across the buying group and confirm all decision-makers and signatories are identified and aligned?

- **1** — The rep is single-threaded; no attempt to identify or align the broader buying group or signatories.
- **2** — Additional stakeholders are acknowledged but not engaged or confirmed.
- **3** — The rep identified some decision-makers but has not confirmed alignment or signing authority.
- **4** — Most decision-makers/signatories are identified and the rep is building consensus, with some stakeholders or sign-off paths unconfirmed.
- **5** — The rep has identified all decision-makers and signatories, is actively building consensus across the group, and has confirmed who signs and who must approve — reflecting that enterprise deals are decided by committee, not by one person.

**Answer guide:** Evaluate consensus-building and signatory mapping, per the playbook objective ('build consensus around it') and the call-type focus ('identifying all decision-makers/signatories, and securing verbal commitment'). The training was emphatic that in enterprise 'there is no single person who's going to get a deal done' — it is by committee. Rate 5 if all decision-makers/signatories are identified, consensus is being actively built, and signing/approval authority is confirmed. Look for: 'who else needs to be comfortable before this moves?', 'who signs the order form, and is anyone above them involved?', evidence of aligning multiple stakeholders. Rate 4 if most are identified with minor gaps. Rate 3 if some are identified but alignment/authority is unconfirmed. Rate 2 if others are merely acknowledged. Rate 1 if single-threaded. Bad examples: assuming the champion is 'the guy' who can sign alone; never confirming who has signing authority.

## 5. Negotiating with Control (Objection Handling & Concessions)

**Question:** How effectively did the rep handle pricing objections and negotiate while holding value, using friction and trading concessions rather than discounting reflexively?

- **1** — The rep conceded on price/terms with little resistance or gave discounts unprompted to keep things moving.
- **2** — The rep handled objections weakly, defending price thinly and conceding without securing anything in return.
- **3** — The rep handled objections adequately but missed opportunities to reinforce value or trade concessions for commitments.
- **4** — The rep negotiated with mostly good control, defending value and trading some concessions, with minor lapses.
- **5** — The rep handled objections by re-anchoring on value, held price with confidence, and traded any concession for a reciprocal commitment (timeline, term length, multi-year, case study, exec sponsorship) — keeping control of the negotiation.

**Answer guide:** Assess negotiation control and disciplined concession-trading, consistent with the playbook ('engagement negotiations') and the training's central theme of control and adding friction/micro-commitments (trading access or commitment for movement). Rate 5 if the rep re-anchors on value when pushed, holds price confidently, and never gives a concession without getting something back. Look for: 'I can look at that if we can commit to a two-year term,' 'help me understand what's driving the concern before we touch price,' refusing to discount reflexively. Rate 4 if control is mostly good with minor lapses. Rate 3 if objections are handled but value isn't reinforced and concessions aren't traded. Rate 2 if the rep concedes without reciprocity. Rate 1 if the rep discounts unprompted or folds quickly. Bad examples: dropping price the moment cost is questioned; offering a discount to 'keep momentum' with nothing in return.

## 6. Equipping the Champion to Sell Internally

**Question:** How effectively did the rep ensure the champion can articulate Encord's value and ROI to economic buyers when the rep isn't in the room?

- **1** — No effort to equip the champion; the rep is relying entirely on their own presence to carry the deal.
- **2** — The rep shared materials but did not check whether the champion can actually articulate the value/ROI.
- **3** — The rep gave the champion some talking points but did not test or reinforce their ability to defend the case internally.
- **4** — The rep equipped the champion with a value/ROI narrative and partially confirmed they can carry it, with minor gaps.
- **5** — The rep deliberately armed the champion with a tailored value/ROI narrative and proof points, tested that they can articulate it (teach-back), and prepared them for likely internal objections — enabling the champion to sell when the rep is absent.

**Answer guide:** Evaluate whether the rep is enabling the champion to sell internally, reflecting the playbook buyer expectation that the buyer 'be able to articulate the value and ROI of Encord,' and the training principle that a champion must 'do work for you without you being in the room.' Rate 5 if the rep equips the champion with a tailored narrative and proof, confirms they can articulate it, and pre-empts internal objections. Look for: 'when your CFO asks why Encord over building in-house, how will you frame it?', providing a one-pager/business case the champion can forward, role-playing the internal pitch. Rate 4 if equipped and partially confirmed. Rate 3 if talking points are shared but not tested. Rate 2 if only materials are shared. Rate 1 if no enablement occurs. Bad examples: assuming the champion will 'figure out' the internal sell; handing over a deck without ensuring they can defend the ROI.

## 7. Securing Verbal Commitment & Mapping the Procurement/Legal Path

**Question:** How effectively did the rep secure verbal commitment to move forward and map the procurement/legal path, owners, and timeline?

- **1** — No verbal commitment sought and no discussion of procurement, legal, or timeline.
- **2** — The rep asked for vague agreement but did not map any of the buying process or timeline.
- **3** — The rep secured soft agreement and touched on procurement/legal but without owners, sequence, or a target date.
- **4** — The rep secured verbal commitment and mapped much of the procurement/legal path and timeline, with some owners or risks unconfirmed.
- **5** — The rep secured clear verbal commitment to proceed and mapped the procurement/legal path — who to be introduced to, vendor portal, security needs, signing authority, and a target close date with any quarter-end/holiday risks flagged.

**Answer guide:** Assess whether the rep converts the proposal into committed forward motion and a mapped path, per the playbook key questions ('who do we need to be introed to for procurement and legal review? what's the timeline on that? do you have a vendor portal?') and the call-type focus on 'securing verbal commitment.' This sets up a clean entry into Legal/Procurement, whose entry criteria include identified procurement/legal stakeholders and an agreed close date. Rate 5 if the rep secures verbal commitment and maps the path (intros, vendor portal, security artifacts, signatory, target date, timeline risks). Look for: 'if we're aligned, who do I work with on procurement and legal?', 'what's realistic for signature, and is anything like quarter-end in play?' Rate 4 if commitment plus most of the path is mapped. Rate 3 if soft agreement with partial mapping. Rate 2 if vague agreement only. Rate 1 if neither commitment nor path. Bad examples: ending the proposal call with 'let us know what you think'; never asking about procurement, signatories, or timeline.

## 8. Using Proof & References to Remove Doubt

**Question:** How effectively did the rep deploy customer references, testimonials, or proof points to remove remaining risk/doubt at the commercial stage?

- **1** — No proof points or references offered, even where the prospect signaled doubt or risk.
- **2** — The rep made a generic claim of having 'lots of happy customers' without anything specific or relevant.
- **3** — The rep referenced a customer or proof point but it was not well-matched to the prospect's industry, use case, or concern.
- **4** — The rep offered relevant proof/references that addressed most concerns, with minor gaps in fit or timing.
- **5** — The rep proactively deployed highly relevant proof — a reference customer in the same vertical/use case, a quantified outcome, or an offered testimonial call — precisely targeted at the prospect's remaining doubt to de-risk the decision.

**Answer guide:** Evaluate use of proof to de-risk the purchase, per the playbook best practice: 'setting up customer testimonial conversation to remove any bit of doubt.' The Demo rubric similarly rewards relevant, situation-specific evidence over generic claims. Rate 5 if the rep deploys a highly relevant reference/proof point (same vertical or use case, quantified result, or an offered reference call) aimed at the specific doubt. Look for: 'we did exactly this with [comparable customer] — happy to set up a call,' citing a quantified outcome that mirrors the prospect's goal. Rate 4 if relevant proof addresses most concerns. Rate 3 if a reference is offered but poorly matched. Rate 2 if claims are generic. Rate 1 if no proof is offered despite doubt. Bad examples: 'trust me, everyone loves it'; offering an unrelated logo as reassurance.

---

## Output JSON shape (what the scorer must produce)

```json
{
  "rubric": "proposal",
  "overall": 3.25,
  "criteria": {
    "delivering_proposal_live":    {"score": 4, "analysis": "..."},
    "tailoring_scope":             {"score": 3, "analysis": "..."},
    "anchoring_price_in_roi":      {"score": 3, "analysis": "..."},
    "building_consensus":          {"score": 2, "analysis": "..."},
    "negotiating_with_control":    {"score": 3, "analysis": "..."},
    "equipping_champion":          {"score": 3, "analysis": "..."},
    "securing_verbal_commitment":  {"score": 4, "analysis": "..."},
    "using_proof_references":      {"score": 3, "analysis": "..."}
  },
  "summary": "...",
  "what_went_well": ["..."],
  "focus_areas": ["..."],
  "next_call_tips": ["..."]
}
```

Each `analysis` is 3-5 sentences with at least 2 attributed direct quotes and one concrete alternative wording the rep could have used (per `agents/call-scorer.md`).
