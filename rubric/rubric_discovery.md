# Discovery Rubric (v1 — Discovery 2025 scorecard from gsheet)

Score each criterion 1-5 using the anchors below. Overall = arithmetic mean of the 7 scores, rounded to two decimals.

Source: [Carl's coaching scorecard gsheet](https://docs.google.com/spreadsheets/d/17Nio3Ql8h-BsXYjkMNcB3DaGmnl9S8R4bf9LEeGJklY/edit?gid=1847499126#gid=1847499126).

Apply this rubric to **Qualification** and **Discovery** calls — the AE is running discovery, qualifying pain / ICP fit / use cases / stakeholders. NOT to demos (use `rubric_demo.md` for those). The scorer must read this file before scoring any Discovery / Qualification call. Output the canonical JSON shape at the bottom.

**Cross-cutting: use `prior_deal_context`.** When `prior_deal_context.verified_via` is set, several criteria below should default lenient if the relevant signal was already established in prior calls / emails / notes. Don't penalize the rep for not re-asking documented questions. Criteria with explicit gates: #2 (Pain), #3 (Current Solution), #6 (Decision-Making), #7 (Why Now). See the inline notes at each of those criteria for details.

---

## 1. Clear Agenda

**Question:** How effectively did the rep set a clear agenda at the beginning of the call?

- **1** — The rep jumped directly into questions or demo without outlining the call structure.
- **2** — Minimal structure was mentioned. Rep may have briefly stated the purpose but didn't outline specific topics.
- **3** — Some agenda was set but lacked detail or confirmation. Rep mentioned what would be covered but didn't ask for buy-in.
- **4** — Most elements were present — outlined topics and confirmed with prospect, but may have missed time expectations or been slightly less detailed.
- **5** — The rep explicitly outlined what would be covered, asked if it worked for the prospect, set time expectations, and did this within the first 5 minutes.

**Answer guide:** Evaluate whether the rep set a clear agenda at the beginning of the call. Look for evidence in the first 5-10 minutes. Rate 5 if the rep explicitly outlined what topics would be covered (such as understanding current workflow, showing platform capabilities, discussing next steps), asked if the agenda worked for the prospect, and set time expectations. Rate 4 if most elements were present — the rep outlined topics and confirmed with the prospect, but may have missed time expectations. Rate 3 if some agenda was set but lacked detail or confirmation. Rate 2 if minimal structure was mentioned. Rate 1 if the rep jumped directly into questions, demo, or product discussion without outlining the call structure. Good examples: "Let me outline what we'll cover today — first understanding your current workflow, then showing how Encord handles annotation, and finally discussing next steps. Does that work for you?" or "We'll kick off with introducing workflows, then cover data selection and labeling, and round off with model evaluation. Please feel free to jump in with questions." Bad examples: immediately asking "What cloud provider do you use?" or launching into product features without any structure.

## 2. Discovery Questions about Current Challenges / Pain Points

**Question:** How thoroughly did the rep ask discovery questions about the prospect's current challenges or pain points?

**Prior-context gate:** If `prior_deal_context.prior_gong_calls[*].brief` / `key_points` or `hubspot_engagements.emails[*].body_excerpt` / `notes[*].body_excerpt` already document the prospect's pain points with specificity, default to at least **3** and note that pain was already established. Score 4-5 if the rep used those documented pain points productively on this call (e.g., "you mentioned in our last call that QA cycles are 3 weeks — has that changed?"). Don't ding the rep for not re-asking documented pain.

- **1** — The rep only asked about tools without asking about problems, or jumped straight to demo without understanding challenges.
- **2** — Only one superficial question about problems was asked. Rep showed minimal interest in understanding challenges.
- **3** — Some basic questions about challenges were asked but lacked depth. Rep touched on problems but didn't probe further.
- **4** — Several good discovery questions were asked about problems and challenges. Rep showed interest in understanding pain points.
- **5** — The rep asked multiple probing questions about challenges, bottlenecks, pain points, and what's not working well. Demonstrated genuine curiosity and dug deeper with follow-up questions.

**Answer guide:** Look for questions like "What are the main challenges you're facing?", "What's not working well with your current solution?", "What problems are you trying to solve?", "What are the biggest bottlenecks?", "What gaps have you seen in other tools?". Rate 5 if multiple probing questions were asked and the rep demonstrated genuine curiosity with follow-ups. Rate 4 if several good discovery questions were asked. Rate 3 if some basic questions were asked but lacked depth. Rate 2 if only one superficial question was asked. Rate 1 if the rep only asked about tools/technical details without asking about problems, or jumped straight to demo without understanding challenges. Good examples include asking about gaps in current tools, what's frustrating about current processes, or what's blocking them. Bad examples include only asking technical questions like "What cloud provider do you use?" without understanding why they need a solution.

## 3. Discovery Questions about Current Solution / Workflow

**Question:** How thoroughly did the rep ask discovery questions about the prospect's current solution or workflow?

**Prior-context gate:** If `prior_deal_context` already documents the prospect's current tooling / workflow (e.g., a prior call brief names "Labelbox" + describes the QA process, or an email thread covers their current pipeline), default to at least **3** and note that current state was already established. Score 4-5 if the rep built on the known state ("last time you mentioned you're using Labelbox for video — has that changed since?"). Score 1-2 only if no prior documentation AND the rep didn't ask on this call.

- **1** — The rep assumed they knew the current state without asking or didn't inquire about existing solutions.
- **2** — Only one superficial question about current tools was asked. Minimal exploration of current state.
- **3** — Some basic questions about current solutions were asked. Rep touched on current tools but didn't go deep.
- **4** — Several questions about current state were asked. Rep demonstrated interest in understanding existing solutions.
- **5** — The rep asked multiple detailed questions about current tools, platforms, workflows, and processes. Showed genuine interest in understanding the current state.

**Answer guide:** Look for questions like "How are you doing this right now?", "What tools are you currently using?", "What does your current workflow look like?", "How do you currently handle annotation?", "What's your current process for data curation?". Rate 5 if multiple detailed questions about current tools / platforms / workflows / processes were asked. Rate 4 if several questions about current state were asked. Rate 3 if some basic questions were asked but didn't go deep. Rate 2 if only one superficial question was asked. Rate 1 if the rep assumed they knew the current state without asking, or launched directly into Encord capabilities. Good examples include asking about current annotation tools, current workflows, how they manage projects today, what platforms they use. Bad examples include jumping into product features without understanding what they currently use.

## 4. Tailoring the Pitch / Demo to What Was Learned

**Question:** How well did the rep adjust or tailor their pitch/demo based on information learned during discovery?

- **1** — The rep gave a generic demo without referencing the prospect's specific situation.
- **2** — Minimal customization with perhaps one reference to prospect's needs. Mostly generic presentation.
- **3** — Some tailoring was evident but limited. Rep may have mentioned one or two things the prospect said.
- **4** — Good customization with several references to prospect's situation. Rep connected some features to stated needs.
- **5** — The rep extensively customized the demo/pitch, explicitly referenced multiple things the prospect said, and connected features to specific pain points mentioned by the prospect.

**Answer guide:** Look for phrases like "Based on what you shared about…", "You mentioned you're struggling with…", "Since you said your priority is…", "Given your use case with…". Rate 5 if extensively customized with multiple references and explicit connections to pain points. Rate 4 if good customization with several references. Rate 3 if some tailoring was evident but limited. Rate 2 if minimal customization with perhaps one reference. Rate 1 if generic demo without referencing the prospect's specific situation, challenges, or use case. Good examples include focusing on specific modalities the prospect mentioned, showing features relevant to stated pain points, or adjusting the demo based on their workflow. Bad examples include showing a standard demo flow without any customization or references to what the prospect shared.

## 5. Clear Next Steps

**Question:** How effectively did the rep establish clear next steps with specific actions or dates?

- **1** — The call ended with no clear next steps or just "get back to you" without timeframe.
- **2** — Vague next steps like "we'll follow up soon" were mentioned without specific dates or actions.
- **3** — Next steps were discussed but lacked specificity (e.g., meeting scheduled but no actions defined, or actions mentioned but no dates).
- **4** — A specific meeting was scheduled OR clear actions with dates were defined. Most elements of good next steps were present.
- **5** — The rep scheduled a specific follow-up meeting with date/time AND outlined specific actions each party would take with timeframes.

**Answer guide:** Look for evidence of scheduling a specific meeting (e.g., "Let's meet Tuesday at 2pm"), defining what will happen before that meeting (e.g., "I'll send over the proposal", "You'll review with your team"), and getting commitment. Rate 5 if both meeting AND actions with timeframes were locked in. Rate 4 if a specific meeting was scheduled OR clear actions with dates were defined. Rate 3 if next steps were discussed but lacked specificity. Rate 2 if vague next steps like "we'll follow up soon" were mentioned without specific dates or actions. Rate 1 if the call ended with no clear next steps. Good examples include scheduling a specific follow-up meeting, defining trial parameters, or outlining what each party will do. Bad examples include ending without scheduling anything or being vague about follow-up.

## 6. Decision-Making Process

**Question:** How effectively did the rep ask about or identify the decision-making process?

**Prior-context gate:** If `prior_deal_context.prior_gong_calls[*]` or `hubspot_engagements.emails[*]` already mapped the buying committee (decision-maker names, procurement / legal stakeholders, budget authority), default to at least **3** and cite the prior context in your analysis. Score 4-5 if the rep referenced known stakeholders productively or pushed on new dimensions (e.g., "last time you named your CTO — has the procurement team also got involved yet?"). Score 1-2 only when no documented decision context exists AND the rep didn't ask.

- **1** — The rep didn't ask about other stakeholders, decision makers, or the approval process.
- **2** — Only one superficial question about decision makers was asked. Minimal exploration of buying process.
- **3** — Some basic questions about who else is involved were asked. Rep touched on decision process but didn't go deep.
- **4** — Several questions about the decision process were asked. Rep showed interest in understanding stakeholders and approval.
- **5** — The rep asked multiple questions about decision makers, stakeholders, approval process, and timeline, and gained clear understanding of the buying process.

**Answer guide:** Look for questions like "Who would be the decision maker?", "Who else needs to be involved?", "What's the approval process?", "When does procurement get involved?", "What's the normal process when buying software?", "Do you need to present this to anyone?". Rate 5 if multiple questions about decision makers, stakeholders, approval process, timeline were asked and clear understanding gained. Rate 4 if several questions about the decision process were asked. Rate 3 if some basic questions were asked but didn't go deep. Rate 2 if only one superficial question was asked. Rate 1 if the rep didn't ask about other stakeholders, decision makers, or the approval process at all. Good examples include asking about decision makers, approval processes, procurement involvement, budget authority, or who needs to sign off. Bad examples include never exploring who else is involved or assuming the person on the call is the sole decision maker.

## 7. Why Now / Replacement vs. New

**Question:** How effectively did the rep uncover why the prospect is speaking with us now, including specific business drivers, and whether they are exploring Encord as a new tool or as a replacement for an existing solution?

**Prior-context gate:** If `prior_deal_context` documents a compelling event (project launch, model release, vendor renewal, regulatory deadline, scale issue) OR clarifies replacement-vs-new posture, default to at least **3** and cite the prior context. Score 4-5 if the rep used the known driver to set urgency or pushed for an updated timeline. Score 1-2 only if no documented driver exists AND the rep didn't probe.

- **1** — No attempt to understand the "why": the rep does not ask why the prospect booked the call, what's happening in the business, or what they're using today. No discussion of new model, project, launch, renewal, or vendor issues. No mention of whether Encord is meant to replace anything or not.
- **2** — Minimal exploration: the rep only touches lightly on "what brought you here today" or "what do you use now", with no follow-up. No real exploration of business drivers, timing, or urgency. No clarity on replacement vs add-on.
- **3** — Partial understanding: the rep asks about current tools or why they're looking now, but not both in enough depth. Business drivers are vague or implied ("we're growing", "exploring options"). It's still unclear whether Encord is new, add-on, or replacement. Little/no explicit confirmation back to the prospect.
- **4** — Most elements are present: the rep identifies at least one specific driver (e.g. upcoming project, new model, or deadline) and current tools. Asks or strongly implies whether Encord is replacing or augmenting. May not summarise clearly or go as deep on impact/urgency as a 5.
- **5** — The rep explicitly uncovers: a clear business driver for evaluating Encord now (e.g. new model launch, upcoming go-live, vendor renewal, scale/quality issues, regulatory requirement); what they're doing today (vendor, in-house tool, manual process); whether Encord is intended as a new tool, add-on, or replacement; and summarises their understanding and checks if it's accurate.

**Answer guide:** Check the first 15-20 minutes for evidence that the rep identified a concrete business driver (e.g. new model release, upcoming launch, vendor renewal, regulatory/compliance need, performance/scale issues), understood the current solution (existing vendor, in-house tool, manual process), clarified whether Encord is intended as a new tool / augmentation / direct replacement, and summarised this back to the prospect ("So what I'm hearing is…"). Rate 5 if all of these are clearly covered and confirmed. Rate 4 if most are present but depth or confirmation is slightly weaker. Rate 3 if only part of the picture is clear (e.g. current tool but no business driver, or vice versa). Rate 2 if the rep only scraped the surface and the real "why now" and replace-vs-new context remain unclear. Rate 1 if there's no meaningful attempt to understand the motivation, business driver, or how Encord is meant to fit.

---

## Output JSON shape (what the scorer must produce)

```json
{
  "rubric": "discovery",
  "overall": 3.43,
  "criteria": {
    "agenda":                     {"score": 3, "analysis": "..."},
    "discovery_pain":             {"score": 4, "analysis": "..."},
    "discovery_current_solution": {"score": 3, "analysis": "..."},
    "tailoring":                  {"score": 3, "analysis": "..."},
    "next_steps":                 {"score": 4, "analysis": "..."},
    "decision_process":           {"score": 3, "analysis": "..."},
    "why_now":                    {"score": 4, "analysis": "..."}
  },
  "summary": "...",
  "what_went_well": ["..."],
  "focus_areas": ["..."],
  "next_call_tips": ["..."]
}
```

Each `analysis` is 3-5 sentences with at least 2 attributed direct quotes and one concrete alternative wording the rep could have used (per `agents/call-scorer.md`).
