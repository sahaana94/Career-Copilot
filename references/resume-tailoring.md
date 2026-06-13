# Resume Tailoring

The goal is a resume that reads like it was written specifically for this role — same person, same real experience, re-prioritized and re-worded so the strongest matches for *this* job are easy to find. Not a different person, and not a rewrite from scratch.

## 1. Find the base resume

Check `Career Profile/profile.md` → Resume Conventions → **Base resume file**. If it's set, use that file as the starting point.

If it's not set, ask the user which file to use (it should be an existing `.docx` resume — editing the user's real formatting is much better than generating a resume from a blank template, since it preserves their layout, fonts, and section structure). Once they point you to one, save that path into `profile.md` so future requests don't need to ask again.

If the user genuinely has no resume at all yet, there's nothing to edit — build a clean first version from scratch using `profile.md`'s Work History, Core Strengths, and Education (a `docx` or `pptx`-adjacent document skill, if available, will help with formatting and layout). Treat that new file as the base resume going forward and save its path into Resume Conventions.

## 2. Plan the changes before touching the file

Read the job description and the relevant parts of `profile.md` (Work History, Core Strengths, Known Gaps, Target Roles & Industries). Identify:

- **Which 3–6 requirements from the JD matter most**, and which existing bullets in the base resume already speak to them (these usually just need re-wording or re-ordering, not replacing).
- **Which bullets are weakest for this particular role** and could be swapped for a different accomplishment from `profile.md`'s Work History that's a better match (only pull from what's actually documented there — don't invent).
- **Whether the summary/headline and the "Core Strengths"-style skills line need updating** to mirror the language and priorities of this JD.
- **Title/positioning framing** — if the profile's "One-line positioning" doesn't quite match this role's framing, the summary is the place to bridge that, honestly.

A quick mental check before writing anything: for every new or reworded bullet, can you point to where in `profile.md` (or its source materials) this comes from? If not, don't write it — ask the user instead.

## 3. Edit the document while preserving formatting

The best results come from editing the existing document's XML directly rather than regenerating it, because it preserves fonts, spacing, bullet styles, and layout exactly.

**If a `docx` skill is available** (check the current skill list), use it: read its `SKILL.md` and follow its unpack → edit `document.xml` → pack → convert-to-PDF workflow. The general shape is:
1. Unpack the `.docx` into its XML parts.
2. Edit the text inside `document.xml` directly (via find-and-replace on the existing paragraph text) — this is just XML, so work carefully with exact string matches and watch for text split across multiple `<w:t>` runs.
3. Repack into a new `.docx`, passing the *original* file so non-text parts (styles, images, layout) come through unchanged.
4. Convert the repacked `.docx` to PDF for the final deliverable.

**If no `docx` skill is available**, fall back to `python-docx`:
- Load the document with `python-docx`.
- Walk `document.paragraphs` (and table cells, if the resume uses tables for layout) to find the paragraphs to change.
- Edit `run.text` on existing runs rather than replacing whole paragraphs, so font/bold/size formatting carries over. If a paragraph's text is split across multiple runs, edit the runs in place and only touch what's necessary.
- Save as `.docx`, then convert to PDF (e.g., via LibreOffice's `soffice --headless --convert-to pdf` if available, or another converter present in the environment).

## 4. Content rules

- **Follow the profile's house style.** Check Resume Conventions in `profile.md` for formatting rules (punctuation conventions, bullet limits, section order, etc.) and apply them to any *new or reworded* content. Pre-existing formatting elsewhere in the template (e.g., how date ranges are formatted) is part of the established design — leave it alone unless the user asks you to change it.
- **Length:** check the page-length norm in Resume Conventions. If the profile says e.g. "2 pages is normal," don't treat 2 pages as a problem to fix — that's the established baseline for this person's resumes. If tailoring pushes the resume noticeably past its normal length, trim content (tighten wording, drop the least-relevant bullet) rather than shrinking fonts/margins, which tends to look worse and breaks consistency with the person's other resumes.
- **Don't fabricate.** Every bullet must trace back to `profile.md` or its source materials. Reframing and re-prioritizing real experience is the job; inventing new accomplishments is not.
- **Match the JD's language where honest.** If the JD says "stakeholder management" and the profile describes the same thing as "cross-functional alignment," it's fine — often better — to mirror the JD's terminology, as long as it accurately describes what the person did.

## 5. Output and file handling

- Name the output clearly, e.g. `[Name]_Resume_[Company].pdf` (match whatever naming convention existing files in the workspace already use, if any).
- If the user has an existing folder structure (e.g., a folder per company), save there. Otherwise ask, or create a sensibly named folder.
- Check Resume Conventions → **Tailored resume output** preference:
  - If "PDF only," delete the intermediate `.docx` working file once the PDF is verified, so the folder contains only the final deliverable.
  - If "PDF + editable file," keep both.
  - If this preference was never set, ask once and save the answer to `profile.md` for next time.

## 6. Verify before handing off

Extract the text from the resulting PDF and sanity-check:
- Page count matches the profile's page-length norm (or is a deliberate, explained deviation).
- No obvious text overflow, cut-off lines, or broken formatting from the edit.
- The summary, skills line, and any reworded bullets read naturally — re-read them as a hiring manager would, not just as a diff.

Then share the file with the user. A short note on what changed and why (1–3 sentences) is more useful than a full diff — they can open the file if they want detail.

## After tailoring

If there's a job description on the table and no fit score has been produced yet for it, it's worth offering one (`references/fit-scoring.md`) so the user knows where they stand. If the user has a contact at the company, offer a referral note (`references/referral-notes.md`).
