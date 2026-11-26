Discovery & Opportunity Assessment: Café Sol Review Radar
Author: Awunti (AI Product Manager) | Version 2 | 24 Nov 2026 | Decision needed from: Laura (Owner)


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