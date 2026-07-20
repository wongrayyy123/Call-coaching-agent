# Demo Rubric (v4 — Encord coaching scorecard from gsheet)

Score each criterion 1-5 using the anchors below. Overall = arithmetic mean of the 8 scores, rounded to two decimals.

Source: [Carl's coaching scorecard gsheet](https://docs.google.com/spreadsheets/d/17Nio3Ql8h-BsXYjkMNcB3DaGmnl9S8R4bf9LEeGJklY/edit?gid=1847499126#gid=1847499126).

The scorer must read this file before scoring any Demo / Evaluation call. Output the canonical JSON shape at the bottom — the keys are stable across rubric revisions.

---

## 1. Features vs. Value

**Question:** How effectively did the rep connect Encord's features to the prospect's specific business outcomes rather than just listing capabilities?

- **1** — The rep predominantly demos Encord features (e.g., SAM 2 segmentation, automated tracking, ontology builder) with little or no mention of how they impact the prospect's workflow. The demo feels like a generic product tour with no connection to business outcomes such as faster model iteration, reduced annotation cost, or improved data quality.
- **2** — Minimal value connection. The rep may briefly state the purpose of a feature but doesn't link it to the prospect's specific challenges or measurable outcomes. Value statements are generic (e.g., "this saves time") without quantifying or contextualizing for the prospect's situation.
- **3** — The rep mentions the value of some Encord features but often defaults to feature-focused explanations without consistently tying them to the prospect's pain points, data pipeline bottlenecks, or measurable outcomes like annotation throughput or model accuracy improvements.
- **4** — Good value mapping. The rep connects most features to outcomes, using language like "this means your team can reduce annotation time by X" or "this directly addresses the QA bottleneck you mentioned." Some features are still shown without a clear value tie-in.
- **5** — The rep consistently communicates the value behind each Encord capability, linking them directly to the prospect's specific data challenges, model performance goals, and operational constraints. The rep actively avoids feature dumps and focuses on how Encord drives measurable impact (e.g., annotation speed, data quality, cost reduction, time-to-production).

**Answer guide:** Rate 5 if the rep consistently ties features like AI-assisted labeling, workflow automation, data curation, or model evaluation back to the prospect's specific goals — e.g., "Because you mentioned spending 3 weeks on QA cycles, let me show you how our automated quality metrics flag label errors before they reach your training pipeline." Rate 4 if most features are tied to outcomes but some are shown without clear business relevance. Rate 3 if value is mentioned but inconsistently — the rep drifts into feature-mode regularly. Rate 2 if the rep occasionally references value but the demo is primarily feature-focused. Rate 1 if the demo is a generic product walkthrough with no connection to the prospect's specific situation. Bad examples include: showing every annotation tool type without asking which the prospect needs, or demoing Index embeddings visualization without explaining how it helps their curation process.

## 2. Clarifying Questions When Prospects Ask About Features

**Question:** How effectively did the rep ask clarifying questions when the prospect inquired about specific Encord features or capabilities?

- **1** — The rep answers feature questions directly without further inquiry or fails to seek clarification, missing critical insights. For example, when asked "Can Encord handle our video data?", the rep immediately demos video annotation without asking about video length, frame rate, annotation type needed, or volume — leaving potential business value unexplored.
- **2** — Minimal clarification. The rep may acknowledge the question but quickly moves to a demo without probing for context. For example, when asked about workflow automation, the rep shows the feature without understanding the prospect's current workflow pain points or team structure.
- **3** — The rep asks some clarifying questions but they are surface-level and don't consistently uncover the prospect's underlying concerns or objectives. For example, the rep asks "What type of data do you work with?" but doesn't follow up on the specific challenges or scale involved.
- **4** — Good clarification. The rep asks relevant follow-up questions that deepen understanding, such as "When you say you need better QA, can you walk me through what your current review process looks like and where it breaks down?" Some opportunities for deeper probing are missed.
- **5** — The rep asks insightful, clarifying questions whenever the prospect inquires about features. These questions aim to fully understand the context of the prospect's inquiry, uncover hidden needs, and redirect the conversation to focus on business outcomes and strategic initiatives. For example: "You mentioned needing DICOM support — are you building in-house, working with radiologists, or integrating with an existing PACS workflow? That'll help me show you the most relevant setup."

**Answer guide:** Rate 5 if the rep consistently turns feature inquiries into discovery moments — e.g., when asked about Encord's RLHF capabilities, the rep asks "What model are you aligning? What does your current preference data collection look like? How many evaluators are involved?" before showing the feature. Rate 4 if the rep asks good follow-ups most of the time but occasionally answers directly without probing. Rate 3 if the rep asks some clarifying questions but they're surface-level and don't reveal deeper needs. Rate 2 if clarification is minimal — the rep quickly pivots to showing the feature. Rate 1 if the rep answers directly without any follow-up, missing opportunities to learn about the prospect's workflow, scale, team structure, or integration needs.

## 3. Ability to Differentiate vs. Competitors

**Question:** How effectively did the rep differentiate Encord from competitors (Labelbox, Scale AI, V7, SuperAnnotate, CVAT, Label Studio) **when competitors were in play** — either raised on this call OR surfaced in `prior_calls_context` for this company?

**Critical gate before scoring:** identify whether a competitor signal exists.

- A competitor signal exists if ANY of these are true:
  - The prospect names a specific competitor on this call (e.g., "we use Labelbox", "we're evaluating Scale", "we're looking at Label Studio").
  - The prospect describes an in-house / homegrown tool they want to replace — that IS a competitor (Encord vs. build-vs-buy).
  - `prior_calls_context` mentions a competitor or in-house tool the prospect surfaced previously.
- If NO competitor signal exists in this call OR prior_calls_context, **rate 3 by default** and note explicitly in the analysis that no competitor was in play. Do NOT penalize the rep for not volunteering competitive positioning unprompted — that's not always good selling. Good reps wait for the signal. The default-3 prevents the harsh "1-2 because no competitor mentioned" pattern that reps have flagged as inaccurate.

**Scoring anchors (only apply when a competitor signal IS in play):**

- **1** — The rep ignores or avoids a competitor that was directly raised. Prospect named a competitor or in-house tool, rep changed subject or gave nothing. Worst case: prior_calls_context surfaced a competitor and the rep doesn't even attempt to position against it.
- **2** — The rep acknowledges the competitor but gives only vague positioning ("we're better", "I think you'll find it easier", "we have more features"). No concrete contrast tied to the prospect's specific use case or what the competitor actually does / doesn't do.
- **3** — The rep names one or two real differentiators but doesn't fully tailor to the prospect's situation. Positioning is generic rather than situational. Also the default score when no competitor signal is in play (see gate above).
- **4** — Good competitive positioning. Multiple relevant differentiators tied to the prospect's specific use case. For example, if the prospect uses Labelbox for video, the rep highlights Encord's unified platform + video-native annotation + frame-accurate tooling. Minor gaps in depth or specificity to the prospect's workflow.
- **5** — Sharp, specific, situational. The rep articulates head-to-head differences in terms of the prospect's exact pain — e.g., "Label Studio handles time series via their XY component, but you can't overlay multiple sensor channels or run similarity search across the full duration — both of which you flagged as the gaps in your in-house tool." Demonstrates deep competitive knowledge AND tight mapping to what the prospect cares about.

**Answer guide:** First state whether a competitor signal was in play. If not in play → rate 3 and say so. If in play → rate against the anchors above. Key competitive angles to listen for when scoring 4-5: unified platform vs. tool fragmentation (Labelbox / Scale split offerings), video-native annotation (frame splitting is a real Labelbox / Label Studio limitation), Physical AI / 3D / LiDAR depth (vs. AV-specialist tools), vendor neutrality (vs. Scale AI post-Meta acquisition), enterprise security / compliance, AI-assisted labeling with SAM 2 / SAM 3 pre-labeling, platform-first control vs. managed services, multi-channel sensor overlay + audio-video sync for time-series customers. The in-house / homegrown-tool case is a real competitor — treat it as such: contrast Encord's pre-built capabilities vs. the engineer-time cost of building and maintaining internal tooling.

## 4. Framing the Conversation Around the Prospect's Priorities

**Question:** How well did the rep frame and structure the demo around the prospect's stated priorities, use case, and data modality?

- **1** — The rep follows a generic demo script that does not account for the prospect's specific use case, data type, or priorities. The demo shows a standard walkthrough (e.g., image annotation → ontology → workflow) regardless of whether the prospect works with video, LiDAR, medical imaging, audio, or text. The conversation feels disconnected from the prospect's needs.
- **2** — Minimal customization. The rep may reference the prospect's industry or data type once but follows a largely standard demo flow. The demo order and emphasis don't reflect what the prospect cares about most.
- **3** — The rep briefly acknowledges the prospect's priorities but does not consistently align the demo with them. Features are sometimes presented out of order or without strong ties to the prospect's top concerns. For example, spending significant time on image annotation when the prospect primarily works with video or 3D data.
- **4** — Good customization. The rep structures the demo around the prospect's primary use case and data modality, with several references to specific things the prospect shared. The demo flow feels intentional. Minor sections may still feel generic or tangential.
- **5** — The rep opens the demo by confirming the prospect's key objectives and priorities, then structures the entire walkthrough around them. Throughout the demo, the rep continually refers back to these priorities — presenting Encord's capabilities in a prioritized order that directly aligns with the prospect's most critical needs. For example, for a robotics team: leading with 3D/LiDAR visualization and multi-sensor annotation, then showing edge case curation in Active, then workflow management for their annotation team.

**Answer guide:** Rate 5 if the rep explicitly confirmed priorities at the start and then built the entire demo around them — e.g., "Based on what you shared about your autonomous driving pipeline, I'm going to focus on three things: how you'd ingest and visualize your multi-sensor data, how our 3D annotation tools work for your LiDAR use case, and how Active helps you find the edge cases that matter most." Rate 4 if the demo is well-customized with several references to the prospect's situation but has some generic sections. Rate 3 if priorities are briefly acknowledged but the demo doesn't consistently reflect them. Rate 2 if the rep makes one or two references but mostly follows a standard script. Rate 1 if the demo is completely generic with no adjustment for the prospect's use case, data type, industry, or team size. Look for whether the rep chose the right product areas to emphasize (Annotate vs. Active vs. Index) based on the prospect's primary pain point.

## 5. Mapping Encord's Value to Core Data Problems

**Question:** How effectively did the rep map Encord's platform capabilities to the prospect's core data pipeline challenges?

- **1** — The rep fails to connect Encord's capabilities to the prospect's core data problems, making the conversation feel disconnected. Features are shown in isolation without linking them to the prospect's real challenges around data quality, annotation bottlenecks, curation gaps, or model evaluation needs.
- **2** — Minimal mapping. The rep shows some features related to the prospect's problem area but the connections are vague or surface-level. For example, mentioning "Encord helps with data quality" without demonstrating how specifically it addresses the prospect's QA challenges.
- **3** — The rep maps some features back to the prospect's problems, but the connections are not always clear or compelling. There is some attempt to align the product with the prospect's data pipeline challenges, but it feels inconsistent or vague in places.
- **4** — Good problem-solution mapping. The rep connects most Encord capabilities to specific problems the prospect described, using the prospect's own language and examples. For example: "You said your team wastes 2 days per week on data wrangling across tools — here's how Index centralizes that." Minor gaps remain.
- **5** — The rep skillfully maps each demonstrated Encord capability back to the prospect's specific data pipeline challenges, using the prospect's own language and pain points. The rep clearly demonstrates how each solution directly addresses these issues, creating a compelling case for Encord's impact on their operations. For example: "You mentioned your annotation team is spending 40% of their time on re-work due to label inconsistencies — let me show you how our automated quality metrics and reviewer workflows catch these errors before they compound downstream."

**Answer guide:** Rate 5 if the rep uses the prospect's own language and examples to demonstrate how specific Encord capabilities solve their problems — showing the full loop from problem to solution to outcome. Rate 4 if most capabilities are well-mapped but some feel detached from the prospect's situation. Rate 3 if mapping is attempted but inconsistent — some features feel relevant, others don't clearly tie back. Rate 2 if connections are surface-level or generic. Rate 1 if the rep shows features without relating them to any stated challenge. Key problems to listen for the rep addressing: annotation bottlenecks, data quality/QA issues, tool fragmentation, inability to find edge cases, slow model iteration cycles, scaling annotation teams, managing multi-modal data, compliance/security requirements, and cost of current tooling.

## 6. Referencing Previous Conversations to Enhance Relevance

**Question:** How effectively did the rep reference prior interactions, discovery insights, or information shared earlier to make the demo more relevant and build trust?

**Critical gate before scoring:** check `prior_calls_context` in the input.

- If `prior_calls_context` is empty OR has only one prior call from the same week (effectively first-touch), **rate 3 by default**. There's nothing meaningful to reference, so don't penalize the rep for not doing it. Note in the analysis that this is a first-touch call.
- If `prior_calls_context` has 1+ substantive prior call(s), score normally against the anchors below — the bar is set by what's actually in `prior_calls_context`.

**Scoring anchors (only apply when `prior_calls_context` has substantive prior calls):**

- **1** — The rep ignores `prior_calls_context` entirely. Specific pain points, stakeholders, decision criteria, or commitments from prior calls go unreferenced. The prospect may need to repeat information. If a prior call captured a budget number, a competitor mention, or a stated priority — and the rep doesn't bring any of it up — that's a 1.
- **2** — Minimal referencing. The rep may make one passing reference to a prior conversation but does not meaningfully integrate prior insights. Major content from `prior_calls_context` goes unused.
- **3** — Some references to previous conversations, but surface-level. E.g., "I know you work with medical images" without building on the specific workflow or pain discussed previously.
- **4** — Several specific insights from `prior_calls_context` are woven in. Continuity and attentiveness are visible. Minor opportunities for deeper integration are missed.
- **5** — The rep weaves the strongest signals from `prior_calls_context` into the demo from the open — pain points, stakeholder names, prior commitments, decision criteria. Example: "In our discovery call you shared that your biggest bottleneck is the 3-week QA cycle and that your CTO wants to cut annotation costs by 50% this year — I've structured today's demo around those two goals."

**Answer guide:** Start the analysis with a one-line note of what `prior_calls_context` contained (e.g., "2 prior calls: discovery surfaced 3-week QA bottleneck + competitor Labelbox + CTO sponsor"). Then score against what the rep did with that material. If `prior_calls_context` is empty, say "first-touch call, no prior context to leverage" and rate 3. Positive signals to listen for: "You mentioned last time…", "Based on what your team shared about…", "When we spoke with [stakeholder name from prior_calls_context]…", "Coming back to the X you flagged earlier…".

## 7. Demonstrating the Right Product Components for the Use Case

**Question:** How effectively did the rep select and demonstrate the right Encord product components (Annotate, Active, Index, Workflows, Data Agents) based on the prospect's specific use case and data pipeline stage?

- **1** — The rep demonstrates a fixed set of product components regardless of the prospect's use case. For example, spending most of the demo on annotation tooling when the prospect's primary pain point is data curation or model evaluation. No attempt to assess which part of the platform is most relevant to the prospect's current pipeline gaps.
- **2** — Minimal component selection. The rep may show the relevant product area briefly but spends disproportionate time on components that don't address the prospect's stated needs. The selection feels default rather than deliberate.
- **3** — The rep shows some relevant product components but does not consistently prioritize the ones most aligned with the prospect's needs. For example, demoing both Annotate and Active but not clearly explaining when or why the prospect would use each, or spending equal time on both when one is clearly more relevant.
- **4** — Good component selection. The rep focuses the demo on the 1-2 product areas most relevant to the prospect and explains how they connect. For example, showing how Index feeds into Annotate for a team that needs to curate before labeling. Minor time spent on less relevant areas.
- **5** — The rep precisely selects and sequences the product components most relevant to the prospect's pipeline stage and use case. They clearly explain why each component matters for the prospect's situation and how they work together. For example, for a team struggling with data quality: leading with Active's quality metrics and label error detection, then showing how Collections send curated data back to Annotate for re-work, and finally demonstrating how Workflows automate this loop — painting a complete picture of how Encord solves their end-to-end problem.

**Answer guide:** Rate 5 if the rep precisely matched product components to the prospect's pipeline gaps and sequenced them logically — showing the prospect a clear path from their current problem to the Encord solution. Rate 4 if the right components are selected but the connection between them could be clearer, or minor time is spent on less relevant areas. Rate 3 if relevant components are shown but equal weight is given to areas of varying relevance. Rate 2 if the selection feels default rather than tailored. Rate 1 if the rep shows a fixed demo regardless of the prospect's use case. Key signals: Did the rep lead with Annotate for teams that need labeling? Active for teams focused on data quality or model evaluation? Index for teams drowning in unstructured data? Workflows and Data Agents for teams needing automation? Physical AI suite for robotics/AV teams? RLHF/alignment workflows for GenAI teams?

## 8. Open-ended Questions After Showcasing Features

**Question:** How effectively did the rep ask open-ended, thought-provoking questions after demonstrating Encord features to engage the prospect and uncover deeper insights?

- **1** — The rep asks few, if any, open-ended questions during or after showing features, leading to a one-sided presentation where the prospect's input is minimal. The demo feels like a lecture rather than a conversation, reducing engagement and insight into the prospect's real needs.
- **2** — Minimal questioning. The rep may ask one or two closed-ended questions like "Does that make sense?" or "Any questions on that?" but does not prompt the prospect to share how they envision using the capability or what concerns they might have.
- **3** — The rep asks some open-ended questions but they are not always focused on driving meaningful insights from the prospect. The conversation may not uncover the full extent of how the prospect would use Encord's capabilities or what barriers to adoption exist.
- **4** — Good questioning. The rep regularly pauses after key feature demonstrations to ask relevant open-ended questions that drive discussion. For example: "How does your team currently handle this step?" or "What would it mean for your timeline if you could automate this?" Some opportunities for deeper probing are missed.
- **5** — The rep consistently asks open-ended, thought-provoking questions after showcasing features (e.g., "How do you see this fitting into your current annotation pipeline?", "If you could automate the edge case identification we just saw, what would that free your team up to focus on?", "What would need to be true for your team to adopt this workflow?"). These questions encourage the prospect to envision how Encord fits within their organization and provide valuable insights into their expectations, adoption barriers, and decision criteria.

**Answer guide:** Rate 5 if the rep consistently pauses after key demonstrations to ask thought-provoking questions that help the prospect envision adoption and reveal concerns — making the demo feel like a collaborative conversation rather than a presentation. Rate 4 if good questions are asked regularly but some demo sections pass without engagement checks. Rate 3 if questions are present but not always insightful — e.g., "Does that make sense?" doesn't count as a strong open-ended question. Rate 2 if questioning is minimal and mostly closed-ended. Rate 1 if the demo is a one-sided presentation with little to no prospect engagement. Strong questions to listen for: "How does your team handle this today?", "What would change if you had this capability?", "Who else on your team would use this?", "What's your biggest concern about switching from your current tool?", "How would this impact your model development timeline?"

---

## Output JSON shape (what the scorer must produce)

```json
{
  "rubric": "demo",
  "overall": 3.25,
  "criteria": {
    "features_vs_value":          {"score": 3, "analysis": "..."},
    "clarifying_questions":       {"score": 2, "analysis": "..."},
    "differentiation":            {"score": 3, "analysis": "..."},
    "framing":                    {"score": 4, "analysis": "..."},
    "value_mapping":              {"score": 4, "analysis": "..."},
    "prior_context":              {"score": 4, "analysis": "..."},
    "right_components":           {"score": 4, "analysis": "..."},
    "open_ended_questions":       {"score": 2, "analysis": "..."}
  },
  "summary": "...",
  "what_went_well": ["..."],
  "focus_areas": ["..."],
  "next_call_tips": ["..."]
}
```

Each `analysis` is 3-5 sentences with at least 2 attributed direct quotes and one concrete alternative wording the rep could have used (per `agents/call-scorer.md`).
