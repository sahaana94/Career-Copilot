# Career Copilot

A Claude Skill that turns Claude into a personal job-search assistant. It learns your background once — from your resume, LinkedIn export, and/or a short conversation — and then uses that to:

- **Score job fit** — paste a job posting and get an honest, structured assessment (0–100) of how well it matches your background, with real strengths and real gaps, not generic encouragement.
- **Tailor your resume** — generate a version of your resume re-prioritized and re-worded for a specific role, using your real experience (no fabrication), output as a polished document.
- **Draft referral notes** — a short, warm message you can send to a contact at a company, asking for a referral or introduction.
- **Build interview prep** — a cheat sheet mapping the job's requirements to your strongest real stories, likely questions, honest gaps to be ready for, and questions to ask the interviewer.

Everything is grounded in a single **Career Profile** file that lives in your own workspace — nothing is sent anywhere else, and you can read, edit, or delete it any time.

## Install

This is a [Claude Skill](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview) — a folder containing `SKILL.md` plus supporting reference files that Claude reads when relevant.

- **Cowork / claude.ai:** download `career-copilot.skill` from this repo's [Releases](../../releases) (or build it yourself — see below) and use the "Save skill" option when you open it.
- **Claude Code:** copy the `career-copilot/` folder (this repo) into your skills directory (e.g. `~/.claude/skills/career-copilot/` for a personal skill, or `.claude/skills/career-copilot/` inside a project).
- **Building the `.skill` file yourself:** from a checkout of this repo, zip the `career-copilot/` folder with a `.skill` extension:
  ```bash
  cd career-copilot && zip -r ../career-copilot.skill . -x ".*"
  ```

## How it works

### First use: one-time setup

The first time you ask Career Copilot to do anything — score a job, tailor a resume, anything — it'll notice you don't have a Career Profile yet and walk you through a short setup:

1. **Share what you have.** A resume (PDF/DOCX), a LinkedIn PDF export, and/or a personal "experience reference" doc with your accomplishments. None are required — Career Copilot can build your profile from conversation alone if you'd rather not upload anything.
2. **Answer a handful of calibration questions** that documents can't capture: what roles/industries you're targeting, your seniority and scope, the gaps you're honestly worried about, and your resume conventions (a base resume to use as a template, formatting preferences, whether you want PDF-only output).
3. Career Copilot writes all of this to `Career Profile/profile.md` in your workspace — a single, readable file that's the source of truth for everything else. Review it, edit it, done.

After that, setup is finished. Every future request reuses the profile.

### Everyday use

Just talk to Claude naturally:

- *"Here's a JD I'm looking at — [paste]. Is this a good fit for me?"*
- *"Can you tailor my resume for this Senior PM role at Acme?"*
- *"I know someone on the data team at Acme — can you draft a referral note for me to send her?"*
- *"I have a phone screen with Acme on Thursday — can you put together a cheat sheet?"*

Career Copilot routes each request to the right workflow and pulls everything it needs from your Career Profile.

### Keeping your profile current

Got promoted? Switched what you're targeting? Just say *"update my profile"* and Career Copilot will ask what changed and update `profile.md` in place — no need to redo the whole setup.

## Repo structure

```
career-copilot/
├── SKILL.md                     # entry point: setup flow + routing
├── references/
│   ├── fit-scoring.md           # the weighted fit-scoring rubric + output format
│   ├── resume-tailoring.md      # how tailored resumes get built
│   ├── referral-notes.md        # referral note template + guidance
│   └── interview-prep.md        # interview cheat sheet template + guidance
└── assets/
    └── profile_template.md      # the structure profile.md is built from
```

## Notes on resume editing

For best results — preserving your resume's existing fonts, layout, and formatting — Career Copilot uses a `docx` editing skill if one is available in your Claude environment (Claude Code, Cowork, and claude.ai with Office skills enabled typically have one). If that's not available, it falls back to editing with `python-docx`. Either way, content is only ever drawn from your Career Profile — Career Copilot won't invent experience you don't have.

## Privacy

Your Career Profile and any uploaded source documents (resume, LinkedIn export, etc.) are saved as plain files in your own workspace — the same place Claude already has access to for your other files. They aren't part of this skill's code and aren't shared anywhere by installing or using it.

## License

MIT — see [LICENSE](LICENSE).
