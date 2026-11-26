#  Café Sol Review Radar — PRD (v0.3)

Note: Interviews were role-played with an AI agent acting as the stakeholders, to practise discovery technique. Café Sol is a simulated business.
-----------------------------------------------------------------------------------------------------------------------------------------
Version	Date	Change	Source
v0.2	26 Nov 2026	Added users and roles, urgent definition, alert routing, delivery and privacy rules, cost ceiling, MVP scope, out-of-scope list	Interviews with Laura, Jordi and Núria; Laura's reply to the readout
v0.3	26 Nov 2026	Channels decided (Telegram + email), Mon/Tue alert rule, digest timing, 90-day first run, 14-day reply window, reply-flow rule, decision log	Follow-up messages with Jordi and Laura
1. Problem statement

Serious reviews (hygiene, allergies, a named staff member) sit unread for 1–3 weeks. By the time anyone sees them, nobody remembers the incident, so the cause can't be found and the team gets generic feedback. Meanwhile, positive reviews that praise staff by name never reach the team.

Evidence: raised by all 3 interviewees, unprompted. One hygiene review sat for 9 days; one allergy review for about 3 weeks.

2. Users and roles
Role	Type	Job	What they get	Channel
Jordi (manager)	Primary user	Acts on same-day issues, coaches staff, builds the schedule	Same-day urgent alerts; weekly patterns by day and shift; praise to share at briefings	Telegram
Laura (owner)	Secondary user	Replies to customers, approves the staffing budget	Draft replies to edit and post; weekly summary; urgent alerts on Mon/Tue	Telegram (alerts, drafts) + email (weekly summary)
Núria and staff	Affected stakeholders (not users)	Serve customers	Nothing directly. Their needs become rules (section 6)	—
3. Scope

In scope (MVP)

Source: Google reviews only (about 80% of reviews)
Languages: Spanish, Catalan, English, French
Classify each review: urgent / routine / positive, plus topic tags
Same-day urgent alerts, weekly summary, draft replies, praise for briefings
First run: analyse the last 90 days of reviews for patterns

Out of scope (MVP)

❌ Posting replies automatically. Laura posts every reply herself, even though the Google API could do it
❌ WhatsApp delivery (paid API, over budget; see decision log)
❌ Any manual data entry by staff, including a staff rota
❌ Staff rankings or leaderboards
❌ Draft replies for reviews older than 14 days
❌ TripAdvisor, Instagram, TheFork (candidates for v2; TripAdvisor is seasonal)
❌ Fixing the counter allergen procedure. This is a physical process, not software. It was escalated to Laura, who agreed to act.
4. Urgent definition

A review is urgent if it mentions any of the following:

Hygiene or illness: dirt, hair or foreign objects, food poisoning, "got sick"
Allergies or dietary errors: allergen, wrong milk or ingredient after a dietary request
A named or clearly identifiable staff member in a negative context

Everything else that is negative is routine (e.g. cold coffee, prices, slow service), and goes to the weekly summary as a pattern.

When in doubt, mark it urgent. A false alarm costs Jordi 1 minute; a missed hygiene review costs reputation. (Recall on urgent matters more than precision.)

5. Alert routing
Review type	Goes to	Channel	When
Urgent (Wed–Sun)	Jordi	Telegram	Same day, during working hours
Urgent (Mon, Tue)	Jordi + Laura	Telegram	Same day
Urgent, arriving at night	Same people as above	Telegram	Next morning, before the first briefing
Routine	Jordi	Telegram	Weekly summary, Thursday 13:00 (before the schedule is built at 15:00)
Routine	Laura	Email	Weekly summary, Sunday evening
Positive, names staff	Jordi	Telegram	In the Thursday summary, for the pre-shift briefing
Every review ≤ 14 days old	Laura	Telegram	Draft reply with a link to the review on Google
Reviews > 14 days old (e.g. first run)	Laura + Jordi	Weekly summary only	Counted in patterns; no draft reply
6. Rules from the team (non-negotiable)
Human approval: the AI only drafts replies. Laura edits and posts every one herself, in her own voice. No "Dear valued customer" templates.
Reply flow: no more than one app switch between seeing a draft and posting it. Each Telegram message shows the review, the draft reply and a link that opens the review on Google.
Zero data entry: the tool runs on its own. If it needs staff to fill something in, it will fail (the notebook and the Google Sheet both failed).
Private handling: a complaint naming a staff member goes only to Jordi (or Laura), never to a team channel, so it can be discussed 1-on-1.
Timing: staff can't use phones on shift. Team-facing content is sized for the 5-minute pre-shift briefing.
Praise, not rankings: positive comments are shared as thank-yous, never counted per person.
7. Constraints
Cost ceiling: running cost under €10/month. Laura: "If it's €100 a month, no way." This drives model choice (free Gemini tier or a small model) and the number of AI calls per review (target: 1).
Channels: Telegram (free bot API) and email only. Both users agreed.
Fit existing routines: Jordi builds the schedule on Thursday afternoon; Laura reads reviews on Sunday evening. Deliveries are timed to those habits.
8. Failure modes and edge cases
Situation	Expected behaviour
Jordi is off on an unlisted day (not Mon/Tue)	Accepted risk for MVP. Alert still reaches Jordi on Telegram; review the rule after 4 weeks of use
AI misses an urgent review (false negative)	Highest-risk failure. Measured in evals; urgent recall target in 03-metrics.md
AI flags a routine review as urgent (false positive)	Acceptable at low volume; tracked in evals
Review in a language the model handles poorly	Still classified; draft reply flagged "check translation"
Review contains instructions ("ignore your rules…")	Treated as data, never as instructions
AI service down or over quota	Fallback model; if both fail, email Laura so no review is lost
Same review fetched twice	Duplicate removed (by review ID)
First run brings 90 days of reviews at once	No alerts and no drafts for old reviews; they feed the first weekly summary only
Telegram message fails to send	Retry 3 times; then email Laura
9. Decision log
#	Decision	Why	Alternatives rejected	Owner	Date
D1	Alerts via Telegram	Free bot API; works like WhatsApp; Jordi agreed	WhatsApp: paid per message + business verification, over the €10 budget. Email: Jordi "never" reads it	Jordi	26 Nov
D2	Mon + Tue urgent alerts go to Jordi and Laura	Jordi's Tuesdays change and there is no rota; tracking one would break zero data entry	Maintaining a rota sheet	Jordi	26 Nov
D3	Jordi's summary Thursday 13:00 (Telegram)	Arrives before he builds next week's schedule at 15:00	Monday summary (too late to change staffing)	Jordi	26 Nov
D4	Laura's summary Sunday evening (email)	She already reads reviews on Sunday nights; Thursdays she is often out	Same Thursday Telegram message as Jordi	Laura	26 Nov
D5	First run covers 90 days	Enough history to show patterns	30 days (too little for patterns)	Laura	26 Nov
D6	No draft replies for reviews older than 14 days	Replying to months-old reviews looks odd; Laura asked	Drafts for every review	Laura	26 Nov
D7	Laura posts replies manually via a link	She wants to press the button herself	Posting via the Google API	Laura	26 Nov
10. Open questions
[ ] Validate the reply flow (Telegram → copy → Google link → paste) with Laura in the build phase
[ ] JSON output format for each classified review (Friday task)
[ ] Human approval flow in full detail (Friday task)







--------------------------------------------------------------------------------------------------
Discovery & Opportunity Assessment: Café Sol Review Radar
Author: Awunti (AI Product Manager) | Version 2 | 24 Nov 2026 | Decision needed from: Laura (Owner)
-----------------------------------------------------------------------------------------------------

1. Executive Summary

Café Sol's three cafés receive about 500 reviews a month. Laura can only read them once a month, in a 4-hour session. As a result, recurring problems go unfixed and urgent issues are missed: Born's Google rating fell from 4.6 to 4.2 in three months, and a hygiene complaint (a hair in a salad) went unseen for 3 weeks.

An auto-reply chatbot would not fix this. Replying to reviews is not Laura's main pain; knowing what to fix is.

Recommendation: run a 6-week pilot of Option D (AI tagging + weekly digest + urgent alerts) at Born, at €0 cost. Automated public replies move to Version 2, with Laura approving every reply before it is posted.


2. Evidence

- Volume vs time: about 500 reviews a month across 3 cafés. Laura reads them once a month, in about 4 hours.
- Business impact: Born's Google rating fell 0.4 stars (4.6 to 4.2) in 3 months.
- Detection delay: a hygiene complaint ("hair in a salad") went unseen for 3 weeks, so the kitchen could not act and the customer got no response.
- Symptom vs root cause: Laura says writing replies is not her main pain. Not knowing what to fix is.

Problem statement:
"Laura cannot see recurring patterns or urgent issues across 500 monthly reviews, so problems go unfixed, critical incidents go unnoticed, and ratings drop, as they have at Born."


3. Options Compared

A. Star-rating dashboard (non-AI)
   What: a weekly chart of average stars per café.
   Impact: Low. Shows THAT ratings drop, not WHY.
   Effort: Low. Risk: Low.
   Verdict: not enough on its own. Cheap, so we include it as a small chart in the digest.

B. Managers tag reviews by hand (non-AI)
   What: each manager reads and tags their café's reviews in a shared sheet every week.
   Impact: Medium. Humans tag accurately.
   Effort: High. About 1.5 hours per manager per week (assumption).
   Risk: Low, but it relies on busy people doing extra work every week, so it is likely to stop.
   Verdict: does not last.

C. Auto-reply chatbot (Laura's initial idea)
   What: AI writes and posts public replies to reviews.
   Impact: Low on the real problem. Laura would still need 4 hours a month of reading to spot trends.
   Effort: Medium.
   Risk: High. A wrong or tone-deaf public reply, for example to a hygiene complaint, damages the brand in front of everyone.
   Verdict: not now. Revisit as Version 2 with human approval.

D. AI tagging + weekly digest + urgent alerts (RECOMMENDED)
   What: AI reads every review, tags it, sends a weekly summary, and flags urgent reviews the same day.
   Impact: High. Shows what to fix and catches urgent issues fast.
   Effort: Medium.
   Risk: Low. Output is internal only; a human decides every action.


4. Should This Be AI? (Option D)

- Needs language understanding?  Yes. Free text in Spanish, Catalan and English, with mixed opinions and sarcasm.
- Volume high enough?             Yes. 500 reviews a month is too many to read well.
- Would simple rules fail?        Yes. Keyword rules miss "we waited forever" = slow service.
- Can we tolerate some mistakes?  Yes. Output is internal and a human checks before acting.
- Data available to test it?      Yes. Past reviews exist.
- Fits cost and privacy limits?   Yes, if we use a free tier and remove personal data first (see Risks).

Verdict: AI is justified for Option D because a human stands between the AI and the customer.


5. What Version 1 Does

Tagging: every review gets one or more topics (food quality, service speed, staff friendliness, price/value, cleanliness, atmosphere, other), a sentiment (positive, neutral, negative) and an urgent yes/no. A mixed review like "great food, terrible wait" counts for both topics instead of becoming one neutral score. The exact customer quote is kept with every tag.

Urgent alerts: sent to Laura within 1 hour, ONLY for hygiene or food safety, foreign objects in food, allergic reactions, injuries, or discrimination. Angry reviews that are not dangerous go to the weekly digest instead.

Weekly digest: every Monday at 8:00. For each café: the top 3 issues with how many reviews mention each, 2-3 real quotes with dates, the change from last week, staff praise, and the small star chart from Option A.

Roadmap:
- Version 1 (now) - Listen and fix: find out why Born's rating dropped and stop urgent issues slipping through.
- Version 2 (later) - Respond with guardrails: AI drafts replies, Laura approves each one before it goes live.


6. Risks and Guardrails

- Personal data sent to the AI provider (GDPR).
  Guardrail: remove emails and phone numbers before any AI call; send only the review text. Check the AI provider's free-tier terms on data use before launch.

- AI makes mistakes (wrong tags, a missed urgent review).
  Guardrail: before launch, test on 60 hand-labelled reviews; the AI must catch 10 out of 10 urgent ones. After launch, a weekly spot check of 10 random reviews.

- Alert fatigue: too many alerts and Laura ignores them.
  Guardrail: alerts only for the 5 urgent categories above; everything else is batched into the digest.

- Over-summarizing: vague summaries hide which dish or shift failed.
  Guardrail: every issue shows real quotes and dates, copied from the reviews, never written by the AI.


7. Success Metrics (measured weekly during the pilot)

- Laura's time on reviews: from about 4 hours a month (irregular) to 15 minutes a week or less.
- Urgent detection time: from 3 weeks to 1 hour or less.
- Digest used: Laura opens it in at least 3 of 4 weeks and rates it useful.
- Insight: the top 2-3 causes of Born's rating drop identified by the end of the pilot.
- Cost: €0.
- Outcome (lagging): Born rating at 4.4 or higher within 3 months. Ratings move slowly and are affected by other things (season, staff changes), so this shows direction, not proof.


8. The Ask

From Laura:
- Approve a 6-week pilot at Born, with a €0 budget.
- 30 minutes a week for feedback.
- Access to the last 3 months of reviews from all 3 cafés.
- Help label 20 reviews, so we agree what "urgent" means.


9. Assumptions and Open Questions

- Born's share of the 500 monthly reviews is not known yet (assumption: about one third).
- The 1.5 hours per manager per week for Option B is an estimate.
- Does the feedback form collect names or emails? To confirm before building.
- Free-tier limits and data terms of the AI provider: to confirm.
-------------------------------------------------------------------------------------

# Discovery Research Findings: Café Sol Review Radar
-----------------------------------------------------------------------------------------
**Document:** `02-research.md`  
**Stakeholders Interviewed:** Laura (Owner), Jordi (Shift Manager), Núria (Front-Line Counter Staff)  
**Original Stakeholder Request:** *"A chatbot to handle customer reviews."*  
**Validated Core Problem:** Critical review latency, unshared positive feedback, and multilingual blind spots prevent timely operational action and hurt staff morale—while manual tracking fails under café tempo.

---

## 1. Cross-Stakeholder Evidence Matrix

| Core Finding | Laura (Owner) | Jordi (Manager) | Núria (Staff) | Evidence Strength |
| :--- | :---: | :---: | :---: | :--- |
| **1. Critical review latency blocks root-cause action** | ✅ | ✅ | ✅ | **Unanimous (3/3 — unprompted)** |
| **2. Positive feedback never reaches front-line staff** | ✅ | ✅ | ✅ | **Unanimous (3/3 — unprompted)** |
| **3. Manual tracking fails; system requires zero data entry** | ✅ | ✅ | ✅ | **Unanimous (3/3)** |
| **4. Strict Human-in-the-Loop (HITL) control over replies** | ✅ | — | — | **Owner Non-Negotiable** |
| **5. Privacy & timing rules govern how feedback reaches the floor** | — | ✅ | ✅ | **Operational Consensus (2/3)** |

---

## 2. Detailed Discovery Findings

### Finding 1: Critical Review Latency Destroys Root-Cause Accountability (3/3 Stakeholders)
* **Evidence:** High-severity reviews—including a 1-star hygiene complaint (*"hair in croissant"*) and a severe allergen error (*"almond cake served on a nut-free order"*)—sat unread for **9 to 21 days**. By the time Laura saw them, neither Jordi nor Núria remembered the customer or shift details.
* **Impact:** Without fresh context, Jordi was forced to guess at causes and deliver generic pre-shift lectures (*"be faster,"* *"tie your hair"*), generating staff resentment while leaving real operational bottlenecks (such as Saturday understaffing when a team member called in sick) unaddressed.
* **Product Implication:** The system must enforce **two-tier severity triage**: same-day escalation for high-severity incidents (hygiene, allergens, named staff) and a **weekly trend digest** for routine operational friction (wait times, coffee temperature, pricing).

### Finding 2: Positive Customer Feedback Is Lost, Hurting Morale & Retention (3/3 Stakeholders)
* **Evidence:** Every stakeholder independently highlighted that staff only ever hear about complaints. A regular customer (*Señora Pilar*) posted a glowing review praising Núria by name in August, which Núria only discovered two months later by chance when the customer mentioned it in person.
* **Impact:** Jordi directly connected this negativity bias to high staff turnover. Both Laura and Jordi confirmed they intend to share positive reviews but consistently forget amid daily service demands.
* **Product Implication:** Automated extraction and routing of **staff praise / kudos** is a core requirement—delivered as simple appreciation rather than a competitive scoreboard (which Núria noted would unfairly penalize back-of-house kitchen staff).

### Finding 3: Manual Workflows Fail Under Café Tempo—Zero Data Entry Required (3/3 Stakeholders)
* **Evidence:** Previous manual habits and workarounds repeatedly failed: Laura skips French reviews and reads English slowly; a plan to print good reviews for the back-room corkboard was never executed; Núria's informal practice of writing `OAT` on cups never reached new hires.
* **Impact:** Any workflow requiring managers or staff to log incidents, tag reviews manually, or enter shift notes will be abandoned under peak-hour pressure.
* **Product Implication:** Review ingestion, multilingual translation (**Spanish, Catalan, English, French**), classification, and routing must operate **100% automatically** with zero manual data entry.

### Finding 4: Strict Human-in-the-Loop Control Over External Replies (Owner Mandate)
* **Evidence:** Although the initial request was for a "chatbot to handle reviews," Laura explicitly rejected automated customer responses (*"That's worse than no answer... my customers know me"*). She welcomed AI-drafted wording assistance, provided she personally reviews, edits, and posts every reply.
* **Product Implication:** Autonomous public posting is an explicit **non-goal**. The system will generate multilingual draft responses inside Laura's approval queue, never publishing directly to review platforms.

### Finding 5: Feedback Delivery Must Respect Privacy and Shift-Floor Rules (Manager & Staff)
* **Evidence:** Núria reported feeling publicly shamed when Jordi raised the croissant complaint in front of the entire lunch shift, and noted that phones are prohibited on the floor during service. Jordi also noted that receiving late-night texts at 11:00 PM at home creates stress with no ability to act until the next shift.
* **Product Implication:**
  * **Named staff complaints** must route privately to Laura and Jordi for **1-on-1 coaching**, never broadcast to the team.
  * **Team-facing updates** (positive kudos and weekly operational patterns) must be formatted for Jordi's **5-minute pre-shift or end-of-shift briefing** rather than mid-shift phone alerts.

---

## 3. Findings Outside Scope (Escalated to Owner)

* **Counter Allergen Handling & Signage Risk:** During the front-line interview, Núria revealed that Café Sol lacks formal counter signage or a mandatory cup-marking SOP for customer allergies—relying purely on staff memory during peak rushes, following a previous near-miss involving an almond cake. Because physical food-safety procedures cannot be solved by a review-triage tool, this operational risk was **documented as out of scope and escalated directly to Laura** for immediate corrective action (e.g., counter allergen signage and mandatory cup-marking onboarding for new staff).

#  Summary to owner/
   Hi Laura! Thank you again for your time, and to Jordi and Núria too. Here's what I learned:

1. Bad reviews arrive too late. The serious ones (hygiene, allergies, a staff member named) sit for 1–3 weeks. By then nobody remembers what happened.

2. Good reviews never reach the team. Customers praise your staff by name, but the team only hears about complaints.

3. Anything that needs extra work doesn't last. So the tool must work on its own, with no forms to fill in.

My idea:
• Jordi gets a message the same day when a serious review comes in
• You both get a short weekly summary (e.g. "3 complaints about slow Saturdays")
• The tool writes a draft reply in the customer's language, and you edit and post it yourself
• Good comments go to Jordi to share at the morning briefing, as a thank-you, never a ranking

One thing outside my tool, but important: there's no allergy procedure at the counter (no sign, no rule for marking cups). I'd suggest fixing this soon. It's a safety risk.

Two questions for you:

Did I get anything wrong, or miss something?
Is this split right: Jordi handles same-day alerts, you handle replies, and you both get the weekly summary?

# Owners reply (Laura)

Laura: "Wow, thank you! I read it twice. Yes, that's exactly it. I didn't know about the allergy thing, that scares me. I'll buy a sign this week and talk to Jordi about the cups.

Your questions:

Nothing wrong. But one thing you missed: Jordi is off on Mondays, and some weeks also Tuesday. If a bad review comes on Monday, who gets the message? Maybe me on his days off?
Yes, the split is good 

And a question for you: how much will this cost? I'm a small café. If it's €100 a month, no way. Something small, okay."