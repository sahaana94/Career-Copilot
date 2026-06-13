# Job Fit Scoring

Read the job description carefully, then read `Career Profile/profile.md`, then produce a structured fit assessment. The goal is to help the user decide where to spend their limited application time and energy — that only works if the score is honest. A score that accurately says "this is a stretch" is more useful than one that says "great fit" and leads to a wasted application, and a score that undersells a genuinely strong match isn't useful either.

## Before scoring

- If `Career Profile/profile.md` doesn't exist yet, go back to `SKILL.md` Step 0 and build it first — you can't score a fit without knowing the person.
- Read the **whole** job description, not just the title. Pay attention to which requirements are framed as "required" vs. "nice to have" / "preferred" — these carry different weight.
- Pull the candidate's relevant context from these profile sections in particular: Identity & Positioning, Target Roles & Industries, Education, Work History, Core Strengths, and Known Gaps.

## Scoring Methodology

Score the role across **six categories**, each 1–10. Then compute a weighted overall score. Finally, apply the Process Advantage modifier if relevant.

### Categories & Weights

| Category | Weight | What to assess |
|---|---|---|
| **Domain / Industry Fit** | 20% | How closely does the industry, sector, product type, or customer base match the profile's Work History and Target Roles & Industries? Score high when the role sits in territory the candidate already operates in; score low when it's an adjacent-but-different domain (e.g., B2B → B2C, regulated → unregulated, enterprise → consumer), and lower still for a genuinely unfamiliar domain. |
| **Core Role Requirements** | 25% | Pull the top 5–7 responsibilities or requirements from the JD and check each one against the profile's Work History. How many has this person actually done — not adjacent-to, but actually done? This is usually the highest-signal category, hence the highest weight. |
| **Functional Depth** | 20% | Does the profile show the *specific* technical or functional expertise the role calls for (a tool, methodology, technical domain, regulatory framework, etc.) — not just general competence in the broad function? |
| **Seniority & Experience Level** | 15% | Does the profile's years of experience, titles, and scope of ownership (see Identity & Positioning → Seniority & scope) match what the role expects? Watch for roles that say "5+ years" when the profile shows 10 — that can cut either way (overqualified risk vs. fine) depending on context. |
| **Education** | 10% | Does the profile's Education section meet what's listed (if anything) as required or preferred? If the JD doesn't mention education at all, this category should score high by default (it's a non-issue) rather than being penalized. |
| **Cross-Functional & Leadership Fit** | 10% | Does the role need things like cross-functional collaboration, leading without authority, people management, executive communication, or stakeholder alignment — and does the profile show a track record of that? |

**These weights are defaults, not gospel.** If a category is structurally irrelevant to a given role (e.g., the JD has zero education requirements and the profile has no gaps there either), it's fine to note that it's a non-factor and let it default to a high score rather than agonizing over it. If you redistribute weights for a good reason, say so explicitly in the output so the math stays transparent.

### Process Advantage (modifier, not scored)

Separately from the six categories, note whether the user has a referral, internal connection, alumni tie, or other process advantage for this specific role — this comes up in conversation, not from the profile, so ask if it's unclear and relevant. Express it as a +/- adjustment to the paper score with a short explanation. A warm referral from someone in a position to advocate can meaningfully move the effective odds even when the paper score is mediocre; a cold application into a role with 500+ applicants might warrant a small negative adjustment in the other direction if that context is useful to the user.

## Output Format

Always produce the assessment in this exact structure:

---

**FIT ASSESSMENT — [Role Title] | [Company]**

| Category | Score | Notes |
|---|---|---|
| Domain / Industry Fit | X/10 | One sentence |
| Core Role Requirements | X/10 | One sentence |
| Functional Depth | X/10 | One sentence |
| Seniority & Experience Level | X/10 | One sentence |
| Education | X/10 | One sentence |
| Cross-Functional & Leadership Fit | X/10 | One sentence |

**Overall Paper Score: XX/100**
[Show the weighted calculation briefly, e.g. "(7×0.20 + 8×0.25 + 6×0.20 + 7×0.15 + 9×0.10 + 8×0.10) × 10 = 73"]

**Process Advantage:** [None / describe the referral or connection and its impact on the effective score]

**Effective Score: ~XX/100**

---

**Top Strengths for This Role**
- [Strength 1 — specific, tied to a real bullet from the profile's Work History]
- [Strength 2]
- [Strength 3]

**Honest Gaps**
- [Gap 1 — name it clearly, don't soften. Draw from the profile's Known Gaps section where relevant, plus anything new this specific JD reveals]
- [Gap 2]
- [Gap 3 if applicable]

**Bottom Line**
[2–3 sentences. Is this a natural fit, a stretch, or a reach? What's the single strongest thing going for the candidate, and the single biggest risk? Would you recommend applying — and if it's a reach, is it a "reach but worth a shot" or a "skip this one"?]

---

## Tone Guidelines

- Be direct and honest. The user is making real decisions — where to spend application time, whether to ask for a referral, whether to negotiate — based on this score.
- Don't inflate scores to be encouraging, and don't deflate them to seem rigorous. A 68 that's accurate is worth more than an 82 that isn't.
- Call out genuine strengths clearly — underselling is just as unhelpful as overselling, and it's demoralizing in a way that doesn't help anyone make a better decision.
- If the JD has a hard requirement the profile clearly doesn't meet (a specific years-of-experience floor, a required certification, a "must have" technical skill that's absent), name it explicitly in Honest Gaps rather than burying it in softer language.
- Keep the whole assessment readable in under two minutes — this is a decision tool, not an essay.

## After scoring

If the score suggests this is worth pursuing, it's natural to offer the next step: "Want me to tailor your resume for this one?" If the score is a clear reach or skip, say so plainly and let the user decide whether they still want to proceed — some people apply to reach roles anyway, and that's their call to make, not something to talk them out of.
