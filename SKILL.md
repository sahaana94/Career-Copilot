---
name: career-copilot
description: Use this skill any time the user is job hunting. Triggers include pasting a job description and asking "is this a good fit", "what's my fit score", "should I apply to this", or "am I qualified for this role"; asking to "tailor my resume for [role/company]" or "make me a resume for this job"; asking to "write a referral note" or "draft a message to my contact at [company]"; and asking to "help me prep for my interview at [company]" or "what questions should I expect". This skill builds and maintains a personal Career Profile (from an uploaded resume, LinkedIn export, and/or a short Q&A) the first time it's used, then reuses that profile to score job fit with a weighted rubric, tailor resumes into polished documents, draft referral notes, and generate interview prep guides — all grounded in the user's real background. Always run the setup flow below if no Career Profile exists yet, even if the user's very first message is just a pasted job posting.
---

# Career Copilot

Career Copilot turns Claude into a personal job-search assistant. It works the same way a good friend with strong editing skills and an honest streak would: it learns your background once, then helps you decide whether a role is worth your time, present yourself well if it is, get a foot in the door through your network, and walk into interviews prepared.

Everything here is grounded in the user's **Career Profile** — a single file built from their resume, LinkedIn, and a short conversation. Never invent experience that isn't in the profile or the source documents. If a job needs something the user doesn't have, say so. The honesty is the value.

## How a session usually goes

1. **Find or build the Career Profile** (Step 0 below). This only needs full setup once; after that it's a quick freshness check.
2. **Figure out what the user is asking for** (Step 1 below) and follow the matching reference file.
3. Capabilities chain naturally: paste a job description → fit score → if it's worth pursuing, tailor the resume → draft a referral note if there's a contact → build interview prep once an interview is on the calendar. After finishing one step, it's fine to suggest the next one, but don't start unrequested work — offer it and let the user decide.

---

## Step 0: Find or build the Career Profile

The Career Profile lives at **`Career Profile/profile.md`** in the user's workspace (create the `Career Profile` folder if it doesn't exist). It's the single source of truth every other capability reads from.

### If a profile already exists

Read it silently and move on to Step 1. Don't re-run onboarding or summarize the whole profile back at the user — just use it. If something in the conversation suggests it's stale (a new job, a new degree, "I just got promoted", etc.), mention that you can update it and offer to do so, but don't force it.

If the user explicitly says something like "update my profile," "I have a new role to add," or "redo my profile from scratch," read the existing `profile.md` first, then do a lighter-weight version of onboarding focused on what changed — ask only about the new information, then edit the file in place rather than rebuilding it from zero.

### If no profile exists yet

This is a one-time setup. Explain briefly what's about to happen — something like: *"Before I can score jobs or tailor anything for you, I need to learn your background. This is a one-time setup — afterward I'll reuse what we build here every time."*

**1. Ask what source material they have.** Any of these help, none are required:
- A resume (PDF or DOCX)
- A LinkedIn profile — either a PDF export ("Save to PDF" from their LinkedIn profile page) or pasted text from the About/Experience sections
- A personal "experience reference" doc — a longer running list of accomplishments, metrics, and bullet points they maintain for resume-writing (many people have one of these even if they don't call it that)

If they have none of these, that's fine — the profile can be built entirely from conversation, just with a few more questions.

**2. Read whatever they provide.** Extract:
- Name, current title, location, years of experience
- Education (degrees, schools, honors, GPA if listed)
- Full work history: company, title, dates, and bullet-level accomplishments — especially anything quantified (%, $, scale, headcount, timelines)
- Skills, tools, certifications, awards

Read PDFs and DOCX files directly with available file-reading tools. If the user pastes a LinkedIn URL instead of an export, note that profile pages usually require login to view — ask them to either export the profile to PDF and upload it, or paste the relevant text directly, rather than trying to browse to it.

**3. Ask the calibration questions a resume can't answer.** These are short and matter a lot — don't skip them:
- **Target roles & industries** — what kinds of roles/companies are they applying to right now? (Free text — this drives the whole "Domain Fit" half of scoring.)
- **Seniority & scope** — what level are they operating at (IC, manager, director, etc.), and does that match their titles, or have they been operating above/below their title?
- **Known gaps** — what do they worry will count against them? (e.g., "no people-management experience," "switching industries," "no advanced degree," "all my experience is at big companies and I'm applying to startups"). People are often more clear-eyed about their own gaps than a resume reveals, and naming these up front makes every fit score more honest.
- **Resume conventions** — do they have a base resume file Career Copilot should use as the tailoring template? Any formatting rules to respect (e.g., a house style that avoids certain punctuation, a preferred page length)? When resumes get tailored, should the final deliverable be PDF only, or do they want to keep the editable file too?
- **Anything else** — career goals, what they're optimizing for (comp, mission, flexibility), companies they're especially excited about, or context that doesn't fit elsewhere.

Mix free-text conversation with the `AskUserQuestion` tool where a question has a natural small set of choices (e.g., seniority level, PDF-only preference). Don't turn this into a long-form survey — a handful of well-chosen questions beats twenty.

**4. Synthesize into `Career Profile/profile.md`.** Follow the structure in `assets/profile_template.md`. Write real, specific content — vague placeholders defeat the purpose. Quantified bullets from the resume/experience doc are gold; keep them close to verbatim since they're often hard-won phrasing.

**5. Show the user a brief summary** of what got captured (a few lines, not the whole file) and invite corrections before treating it as final. If they uploaded source files, save copies into `Career Profile/source-materials/` so they're available later (e.g., as raw material for resume tailoring, or to re-run onboarding after a career change) — skip creating that folder if nothing was uploaded.

**If the user's first message already includes both background info and something actionable** (most commonly: a pasted job description), don't let onboarding block that request. Build as much of the profile as you can from what they've already told you, ask only the calibration questions that materially change the answer to what they're asking right now, note in the profile that any unanswered fields are placeholders to fill in later, and then go ahead and do the thing they asked for in the same response. Someone who pastes a job description wants to know where they stand, not to complete a multi-step interview first.

Once the profile is saved, move to Step 1 with whatever the user originally asked for.

---

## Step 1: Route the request

| User says something like... | Go to |
|---|---|
| Pastes a job description, with or without "is this a good fit / what's my score / should I apply / am I qualified" — this is also the **default** when someone pastes a JD with no other instruction | `references/fit-scoring.md` |
| "Tailor my resume for this," "make me a resume for [role/company]," "update my resume to match this JD" | `references/resume-tailoring.md` |
| "Write a referral note," "draft a message to my contact at [company]," "help me ask [name] for a referral" | `references/referral-notes.md` |
| "Help me prep for my interview at [company]," "what should I expect," "build me a cheat sheet for this interview" | `references/interview-prep.md` |

If a request spans more than one of these (common — e.g., "score this and if it's good, tailor my resume"), do them in the logical order and read each relevant reference file before starting that part.

---

## General principles

- **Honesty over flattery.** The whole point of this skill is to help the user make good decisions about where to spend their time and how to present themselves. An accurate score that stings is more useful than a flattering one that misleads. Never inflate fit scores, soften real gaps into non-statements, or claim experience the profile doesn't support.
- **Never fabricate experience.** Every claim in a tailored resume, referral note, or interview talking point must trace back to something in the Career Profile or its source materials. If a job wants something the user genuinely doesn't have, say so — don't paper over it with vague language.
- **Respect the user's existing organization.** Many users keep a folder per company or per application. Before creating new files, check whether a relevant folder already exists (e.g., search for the company name in the workspace) and follow the existing pattern if there is one.
- **Keep the profile current.** If, during any capability, the user shares new information about their background (a new project, a metric they forgot to mention, a change in what they're targeting), offer to fold it into `profile.md` so future sessions benefit too.
- **Don't over-ask.** Setup is a one-time cost. Once the profile exists, most requests (paste a JD, ask for a tailored resume) should need zero or one clarifying question, not a fresh interview every time.
