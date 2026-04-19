# CODE PREP ASSISTANT
## Cowork Skill — Henrik Host / ThreeSixtyOne

TRIGGER: Use this skill at the start of any new build session.
Trigger phrases: "start a new project", "get ready to code", "set up the project",
"prep for Claude Code", "create CLAUDE.md", "build this", "I want to build [X]",
or any time a new coding session begins.

This skill is project-neutral. It runs the same way every time, for every project.

---

## WHAT THIS SKILL IS

This is Henrik's code prep assistant. His foundational instantiation before any build.
It exists so Claude Code opens a project and immediately knows exactly what to do.

It collects:
- What we're building and why
- Tech stack, auth, database, hosting, environment variables
- Design system and brand tokens
- Content sources and local reference files
- The exact build order and instruction for Claude Code

The output is a fully loaded local project folder.
Claude Code opens it cold and enters plan mode immediately.
No back and forth. No explaining context. No guessing.

---

## HOW IT RUNS

Work through 8 checkpoints in order.
For each checkpoint: ask if it's already done.
YES — take it, move on.
NO — ask ONE targeted question to fill the gap. Never more than one.
Done in under 10 minutes.

---

## CHECKPOINT 1 — THE BRIEF

Ask: "Do you have a brief, PRD, or description of what we're building?"

- YES — take it (paste, doc link, summary). Extract: what it does, who it's for, core purpose.
- NO — ask: "Give me the idea in 2-3 sentences." Structure it into a one-paragraph brief.

Capture: project name, one-sentence purpose, intended audience.

---

## CHECKPOINT 2 — CLARITY

Ask: "Is the purpose, audience, and scope clear enough to start building?"

- YES — move on.
- NO — ask the ONE most important missing question. Capture the answer. Move on.

One question maximum. This is not a full discovery session.

---

## CHECKPOINT 3 — RESEARCH

Ask: "Does this need market or feasibility research before we start?"

- YES — run the research-gate skill, return here with findings.
- NO — skip entirely.

Most projects skip this. Only run it if the idea's viability is genuinely unclear.

---

## CHECKPOINT 4 — PRIORITY

Ask: "Is this the right thing to build right now?"

- YES — move on.
- NOT SURE — quick score: real problem? feasible? fits portfolio?
  Rate HIGH / MEDIUM / LOW. Confirm before continuing.

---

## CHECKPOINT 5 — USER FLOW

Ask: "Do you have a user flow or journey map for this?"

- YES — take it. Summarise the key steps.
- NO — ask: "Who uses this? What's the first thing they do? What's the outcome?"
  Build a 5-step flow from the answers.

Capture: the core user journey as a numbered list.

---

## CHECKPOINT 6 — SCREENS AND FEATURES

Ask: "Do you know what screens or features this needs?"

- YES — take the list.
- NO — derive from the user flow. List implied screens. Confirm: "Does this cover it?"

Capture: numbered list of screens/sections in intended build order.

---

## CHECKPOINT 7 — VISUAL REFERENCE

Ask: "Do you have a mockup, prototype, or visual direction?"

- YES — note the reference.
- NO — ask: "Which design system applies?"

Options:
  A. ATLASdesign — Henrik's own products (HostAtlas, Reviews361, Workshop361)
  B. GS1 Official Brand — GS1 Norway client work only
  C. Other client brand — collect exact hex values and font names now
  D. New system needed — note it, define later in build

Capture: design system name + any specific token overrides.

---

## CHECKPOINT 8 — TECHNICAL SETUP

Always runs fully. Ask each item only if not already known.

8a. REPO
"What is the GitHub repo name?"
Format: 361Henrik/repo-name
If it doesn't exist: create it now using the GitHub connector.

8b. LOCAL FOLDER
"What is the local folder path on your Mac?"
Example: ~/Developer/active/project-name

8c. LIVE URL
"What is the target live URL?"
Example: playbook.gs1.threesix1.com
Note: DNS is managed in Squarespace (threesix1.com) or the client's domain manager.

8d. AUTH / SIGN-IN
"Does this need user authentication?"
- YES — Supabase Auth. Env vars: VITE_SUPABASE_URL + VITE_SUPABASE_ANON_KEY
- NO — skip

8e. DATABASE
"Does this need a database?"
- YES — Supabase (PostgreSQL). Ask: existing project or create new?
  Schema goes in supabase/schema.sql
- NO — skip

8f. AI FEATURES
"Does this need AI features — chat, generation, analysis, Claude API?"
- YES — note which features. Env var: VITE_ANTHROPIC_API_KEY
  Model: claude-sonnet-4-20250514
- NO — skip

8g. OTHER SERVICES
"Any other services? Stripe, email, file storage, third-party APIs?"
- Note each one with its required env var name.

8h. DESIGN TOKENS
Based on Checkpoint 7, insert the exact token set:

ATLASdesign (Henrik's own products):
  --atlas-canvas:      #F6F3EE   /* 80%+ of visible area */
  --atlas-stone:       #E8E2D9   /* cards, panels */
  --atlas-charcoal:    #1A1F1A   /* all body copy, headings */
  --atlas-muted:       #6E6A5E   /* captions, supporting labels */
  --atlas-green:       #1F4A3A   /* nav, identity panels — never CTA */
  --atlas-terracotta:  #C35C3C   /* CTAs on light surfaces only */
  --atlas-bronze:      #C9A962   /* CTAs on dark surfaces, icon highlights */
  --atlas-border:      #CCC4B8   /* cards, inputs, dividers */
  Fonts: Playfair Display (headings, weight 500) + Lexend (body, weight 400/500)

GS1 Official Brand (client work):
  --gs1-blue:          #003087   /* primary — headings, nav */
  --gs1-orange:        #F26334   /* accent only — underlines, bullets */
  --gs1-bg:            #F5F5F5
  --gs1-surface:       #FFFFFF
  --gs1-border:        #E0E0E0
  --gs1-text:          #1A1A1A
  --gs1-text-muted:    #5C5C5C
  --gs1-blue-light:    #E6EDF5   /* active nav background */
  Fonts: Montserrat (headings — Gotham equivalent) + Inter (body)

Custom: use values collected in Checkpoint 7.

---

## OUTPUT — CREATE THESE FILES

Once all 8 checkpoints are complete, produce the following.
Push to GitHub. Show each file to Henrik for confirmation.

---

### FILE 1: CLAUDE.md (at project root)

This is the single most important file. It is what Claude Code reads.
It must be complete. No placeholders. No TODOs.
If something wasn't established, write "TBD" and flag it explicitly.

```
# CLAUDE.md — [Project Name]

---

## HOW I WORK — NON-NEGOTIABLE

- Plan mode first. Read this file fully. Show a numbered plan. Wait for approval. Then build.
- Design before backend. Tokens → shell → sections/screens → features → then API wiring.
- One section at a time. Build it, show it, wait. Do not rebuild approved things.
- Run `npm run build` before every commit. No broken builds ever pushed to main.
- Commit format: feat: / fix: / chore: / docs:

---

## TECH STACK

Frontend:    React 19 + TypeScript + Vite 6 + Tailwind CSS v4
Icons:       Lucide React
Animation:   Framer Motion (imported as 'motion')
Auth:        [Supabase Auth | None]
Database:    [Supabase | None]
AI:          [Anthropic Claude API claude-sonnet-4-20250514 | None]
Deploy:      Vercel — GitHub main branch auto-deploy
Live URL:    [URL]
Repo:        https://github.com/361Henrik/[repo-name]

---

## SETUP CHECKLIST

Before writing any code, verify all of these:
- [ ] `npm install` — no errors
- [ ] `.env.local` exists with all values filled in
- [ ] `npm run dev` — loads on localhost:3000
- [ ] `npm run build` — no TypeScript errors

---

## PROJECT

**What it is:** [one sentence — what it does and for whom]
**Core purpose:** [why it exists — what problem it solves]
**Audience:** [who uses this]
**Key outcome:** [what users should think, feel, or do after using it]

---

## DESIGN SYSTEM

[Full CSS @import and @theme block with all tokens]
[Typography rules: heading font, body font, weights]
[Component rules: card style, CTA rules, sidebar behavior if applicable]

---

## USER FLOW

[Numbered 5-step flow from Checkpoint 5]

---

## SCREENS / SECTIONS TO BUILD

[Numbered list in build order from Checkpoint 6]
1.
2.
3.

---

## BUILD ORDER

Follow this exact sequence. Do not skip ahead.
1. src/index.css — full design token replacement
2. src/App.tsx — shell, navigation, layout
3. [Each screen/section in order]
Final: npm run build → fix all errors → commit → push to main

---

## ENVIRONMENT VARIABLES

[Keys only — no values. All values live in .env.local]
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=
VITE_ANTHROPIC_API_KEY=
[any others from Checkpoint 8g]

---

## CONTENT SOURCE

[Where does content come from?]
[If a local file exists: docs/content-source.md — read it before building any section]
[Language requirements if Norwegian: confirm tone, formality level]

---

## THE ASK

> Read CLAUDE.md fully. Read docs/content-source.md if it exists.
> Enter plan mode. Show me a numbered build plan.
> Flag any gaps or risks you see in the current codebase.
> Do NOT write any code yet. Wait for my approval.
```

---

### FILE 2: vercel.json

```json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }],
  "buildCommand": "npm run build",
  "outputDirectory": "dist",
  "framework": "vite"
}
```

### FILE 3: .env.example

All env var keys from Checkpoint 8. No values.

### FILE 4: .gitignore

```
node_modules
dist
.env.local
.env
.DS_Store
```

### FILE 5: docs/content-source.md

Create this only if the project has content Claude Code needs to read.
Write here: Norwegian text, section copy, content structure, brand guidelines.
This replaces the need to share Google Docs during a Claude Code session.

### FILE 6: supabase/schema.sql

Create this only if a database is needed.
Write the initial schema based on what was gathered in the brief.
Claude Code runs this in the Supabase SQL Editor.

---

## HANDOFF MESSAGE

After all files are ready, say exactly this to Henrik:

---
"Ready. Here's what to do:

1. cd [local-folder-path]
2. git pull origin main  (or git clone [repo-url] if new)
3. npm install
4. cp .env.example .env.local — fill in the values
5. Open Claude Code Desktop → Open Project → [local-folder-path]
6. Paste this as your first message:

   Read CLAUDE.md fully. Read docs/content-source.md if it exists.
   Enter plan mode. Show me a numbered build plan.
   Do NOT write any code yet. Wait for my approval.

You're ready."
---

---

## HENRIK'S DEFAULTS

Apply these to every project unless a checkpoint overrides them.

- GitHub org: 361Henrik
- Stack: React 19 + TypeScript + Vite 6 + Tailwind CSS v4 + Lucide + Framer Motion
- Deploy: Vercel, auto-deploy from main branch
- Domain pattern: subdomain.threesix1.com (DNS in Squarespace)
- Database: Supabase if needed
- AI: Anthropic Claude API if needed
- Auth: Supabase Auth if needed
- No broken builds. Ever.
- Commit format: feat: / fix: / chore: / docs:

---

## THIS SKILL WORKS FOR ALL PROJECT TYPES

- Client work (GS1 Norway, others) — client brand system
- HostAtlas / Helmut / Olga — ATLASdesign
- Reviews361 — ATLASdesign
- Workshop361 — ATLASdesign
- New SaaS or tools — ATLASdesign or new system
- Quick demos or prototypes — lightweight setup, same 8 checkpoints

The checkpoints are the same every time.
The outputs adapt to what each project needs.
