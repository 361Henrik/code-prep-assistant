Code prep assistant — Henrik's foundational pre-flight before any Claude Code session. Use this skill at the start of any new build session. Trigger phrases: "start a new project", "get ready to code", "set up the project", "prep for Claude Code", "create CLAUDE.md", "build this", "I want to build", "new project setup", or any time a new coding session begins. Project-neutral — runs the same way every time for every project.

# CODE PREP ASSISTANT
## Henrik Host / ThreeSixtyOne — Foundational Build Instantiation

This skill produces the best possible input for Claude Code.
It is project-neutral. It runs the same way every time.
The output is a fully loaded local project folder Claude Code opens cold and enters plan mode immediately.

---

## BEFORE THE CHECKPOINTS — ASK FOR DOCUMENTS FIRST

Always start here before anything else:

"Do you have anything to share before we start?
A brief, PRD, design file, screenshot, brand guide, content doc, reference, or upload?
Drop everything here first — I'll read it all before asking a single question."

Read every document shared. Extract relevant information into the checkpoints automatically.
Save all documents to docs/ in the local project folder.
Name them clearly: brief.md, content.md, brand-guide.md, user-research.md, design-ref.md, etc.
Claude Code reads everything in docs/ before writing a single line.

---

## ALSO CHECK — EXISTING CODEBASE

Ask: "Does a codebase already exist for this project, or are we starting from scratch?"

- EXISTING — ask for the repo URL and local path. Note what's already built so Claude Code doesn't rebuild it.
- SCRATCH — proceed. Claude Code starts fresh.

---

## 10 CHECKPOINTS

Work through all 10 in order.
For each: ask if it's already known or done.
- YES / already in documents — take it, move on.
- NO — ask ONE targeted question. Never more than one at a time.

Target: done in under 15 minutes.

---

## CHECKPOINT 1 — THE BRIEF

"Do you have a brief, PRD, or description of what we're building?"

- YES — extract from documents or paste. Pull: what it does, who it's for, core purpose.
- NO — "Give me the idea in 2-3 sentences." Structure it into a one-paragraph brief.

Capture:
- Project name
- One-sentence purpose
- Intended audience
- Core problem it solves
- Key outcome for the user

---

## CHECKPOINT 2 — CLARITY

"Is the purpose, audience, and scope clear enough to build from?"

- YES — move on.
- NO — ask the ONE most important missing question. One only.

---

## CHECKPOINT 3 — RESEARCH

"Does this need feasibility or market research before we start?"

- YES — run research-gate skill. Return here with findings.
- NO — skip.

---

## CHECKPOINT 4 — PRIORITY

"Is this the right thing to build right now?"

- YES — move on.
- NOT SURE — score it: real problem? technically feasible? fits current focus?
  Rate HIGH / MEDIUM / LOW. Confirm before continuing.

---

## CHECKPOINT 5 — USER FLOW

"Do you have a user flow or journey map?"

- YES — take it. Summarise into 5-7 numbered steps.
- NO — ask: "Who uses this, what's the first thing they do, and what's the end outcome?"
  Build the flow from the answers. Offer to run user-flow-mapper for a visual.

Capture: numbered step-by-step user journey.

---

## CHECKPOINT 6 — SCREENS AND FEATURES

"Do you know what screens or features this needs?"

- YES — take the list.
- NO — derive from the user flow. List implied screens. Confirm: "Does this cover it?"

Capture: numbered list of screens/sections in build order.
Tag each as: MVP / Phase 2 / Later.
MVP should be ruthlessly small — max 6 screens.

---

## CHECKPOINT 7 — VISUAL REFERENCE AND DESIGN SYSTEM

"Do you have a mockup, prototype, screenshot, or visual reference?"

- YES — note it. Ask: "Should I build a clickable prototype before we hand off to Claude Code?"
  If yes — run visualize-prototype skill. Approved prototype becomes a reference in docs/.
- NO — ask: "Which design system applies?"

ALWAYS collect these regardless:
- Primary colors (hex values)
- Secondary / accent colors (hex values)
- Background and surface colors (hex values)
- Font for headings (name + weights)
- Font for body text (name + weights)
- Border radius default
- Component rules (card, button, nav, inputs)

ATLASdesign tokens (Henrik's own products — use if confirmed):
```css
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@500&family=Lexend:wght@300;400;500&display=swap');
@import "tailwindcss";

@theme {
  --color-atlas-canvas:     #F6F3EE;
  --color-atlas-stone:      #E8E2D9;
  --color-atlas-charcoal:   #1A1F1A;
  --color-atlas-muted:      #6E6A5E;
  --color-atlas-green:      #1F4A3A;
  --color-atlas-terracotta: #C35C3C;
  --color-atlas-bronze:     #C9A962;
  --color-atlas-border:     #CCC4B8;
  --font-display: 'Playfair Display', serif;
  --font-sans:    'Lexend', system-ui, sans-serif;
}
```

For client or new projects: collect ALL values and write an equivalent block.
Save to docs/design-system.md as well.

Capture: complete CSS token block ready to paste into src/index.css.

---

## CHECKPOINT 8 — CONTENT AND LANGUAGE

"Does this project have content Claude Code needs to use when building?"

- YES — ask:
  - What language? (English, Norwegian, other?)
  - What tone? (Formal, warm, editorial, conversational?)
  - Where does it come from? (Paste / Google Doc link / already in docs/)
  Write all content to docs/content.md.
- NO — skip.

Also ask: "Any SEO, accessibility, or localisation requirements?"

---

## CHECKPOINT 9 — TECHNICAL SETUP

Always runs fully. Ask each item only if not already known.

### 9a. Repo
Format: 361Henrik/repo-name. Create via GitHub connector if needed.

### 9b. Local folder
Common: ~/Developer_ClaudeCode/ or ~/Developer/active/

### 9c. Live URL and domain
Ask — never assume. Note where DNS is managed.

### 9d. Vercel
Existing project or new? Note project name and team.

### 9e. Auth
- YES — Supabase Auth. VITE_SUPABASE_URL + VITE_SUPABASE_ANON_KEY. Email/password or social login?
- NO — skip.

### 9f. Database
- YES — Supabase. Existing (get URL + region) or new? Schema in supabase/schema.sql.
- NO — skip.

### 9g. AI features
- YES — which features? VITE_ANTHROPIC_API_KEY. Model: claude-sonnet-4-6.
  Run ai-invocation-builder for prompt specs if needed.
- NO — skip.

### 9h. Other services
Stripe, email, storage, maps, third-party APIs? Note each with env var name.

### 9i. Versions
- Node 20+, React 19, Vite 6, Tailwind v4, TypeScript strict
- Tailwind v4: uses @import "tailwindcss" and @theme {} — NOT tailwind.config.js
- Framer Motion: import { motion } from 'framer-motion'

### 9j. Existing integrations
Analytics, CRM, monitoring, support tools? Note each.

---

## CHECKPOINT 10 — FINAL CONFIRMATION

Read back a one-paragraph summary of everything collected.
"Does this cover it? Anything missing or wrong?"
Do not proceed to file creation until Henrik confirms.

---

## OUTPUT — CREATE ALL THESE FILES

---

### FILE 1: CLAUDE.md (project root)

Complete. No placeholders. No TODOs. Claude Code reads this first.

```markdown
# CLAUDE.md — [Project Name]
Last updated: [date]

---

## HOW I WORK — NON-NEGOTIABLE

- Read this file fully before doing anything else.
- Read every file in docs/ before writing any code.
- Plan mode first. Show a numbered build plan. Wait for approval. Then build.
- Design before backend: tokens → shell → screens → features → API wiring.
- One screen at a time. Build it. Show it. Wait. Do not rebuild approved screens.
- Run `npm run build` before every commit. No broken builds ever pushed to main.
- Commit format: feat: / fix: / chore: / docs:
- If you hit a decision not covered here, stop and ask. Do not guess.

---

## PROJECT

**Name:** [project name]
**What it is:** [one sentence]
**Core purpose:** [why it exists]
**Audience:** [who, their context]
**Key outcome:** [what the user should be able to do or feel]
**Language:** [English / Norwegian / other + tone notes]

---

## EXISTING CODEBASE

[Starting from scratch.]
OR
[Existing repo: [URL]. Already built: [list]. Do NOT rebuild these.]

---

## TECH STACK

Frontend:    React 19 + TypeScript (strict) + Vite 6 + Tailwind CSS v4
Icons:       Lucide React
Animation:   Framer Motion — import { motion } from 'framer-motion'
Auth:        [Supabase Auth | None]
Database:    [Supabase PostgreSQL | None]
AI:          [Anthropic claude-sonnet-4-6 | None]
Deploy:      Vercel — auto-deploy from main
Node:        20+

Live URL:    [URL]
DNS:         [where managed]
Repo:        https://github.com/361Henrik/[repo-name]
Vercel:      [project name]

Tailwind v4: uses @import "tailwindcss" and @theme {} — NOT tailwind.config.js

---

## SETUP — BEFORE WRITING ANY CODE

1. npm install — zero errors required
2. cp .env.example .env.local — fill in every value
3. npm run dev — confirm loads on localhost:3000
4. npm run build — zero TypeScript errors required
5. Read every file in docs/ — required before touching any code

If any step fails: stop and report. Do not work around silently.

---

## ENVIRONMENT VARIABLES

[All keys — values in .env.local, never committed]
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=
VITE_ANTHROPIC_API_KEY=
[others]

---

## DESIGN SYSTEM

[Full @import and @theme block — exact CSS, paste into src/index.css]

Typography:
- Headings (h1–h3): [font], weight [X]
- Body / UI: [font], weight [X]

Component rules:
- Cards: [border-radius, border, background, padding]
- Primary CTA: [color, hover]
- Secondary CTA: [color, hover]
- Nav: [background, text, active state]
- Inputs: [border, focus, border-radius]

---

## DOCS FOLDER — READ ALL OF THESE FIRST

[List every file in docs/ with one-line description]
- docs/brief.md — project brief
- docs/content.md — all copy and content per screen
- docs/design-system.md — full token reference
- docs/user-flow.md — step-by-step user journey
- docs/prototype.md — approved prototype reference
[add others]

---

## USER FLOW

[Numbered 5-7 step journey]

---

## SCREENS TO BUILD

| # | Screen | Purpose | Tag |
|---|--------|---------|-----|
| 1 | [name] | [one line] | MVP |
| 2 | [name] | [one line] | MVP |

Build MVP screens only this session.

---

## BUILD ORDER

1. src/index.css — full token block. Verify fonts load.
2. src/App.tsx — shell, layout, navigation
3. [Screen 1]: [what to build]
4. [Screen 2]: [what to build]
[continue for all MVP screens]
Final: supabase schema → auth → AI → npm run build → fix errors → commit → push

---

## DATABASE

[If Supabase]
Project URL: [URL]
Region: [region]
Schema: supabase/schema.sql — run in Supabase SQL Editor before coding

---

## AI FEATURES

[If Claude API]
Model: claude-sonnet-4-6
Specs: docs/ai-specs.md

---

## THIRD-PARTY INTEGRATIONS

[List with brief setup note each]

---

## THE ASK

> Read this file fully.
> Read every file in docs/.
> Check the existing codebase (if any).
> Enter plan mode: show a numbered build plan for all MVP screens.
> Flag any gaps, risks, or missing information.
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
All env var keys. No values.

### FILE 4: .gitignore
```
node_modules
dist
.env.local
.env
.DS_Store
*.log
```

### FILE 5: docs/ folder
Every project gets this. Populate with everything collected.
- docs/brief.md
- docs/content.md (if content exists)
- docs/design-system.md
- docs/user-flow.md
- docs/prototype.md (if prototype was built)
- docs/ai-specs.md (if ai-invocation-builder was run)
- Any uploaded documents — renamed clearly

### FILE 6: supabase/schema.sql
Only if database needed. Include CREATE TABLE, RLS policies, indexes.

---

## PRE-HANDOFF QUALITY CHECK

Run this before the handoff message. Do not hand off if anything is unchecked.

BRIEF
- [ ] Project name confirmed
- [ ] One-sentence purpose written
- [ ] Audience defined
- [ ] Core problem clear
- [ ] Key outcome defined
- [ ] Language and tone confirmed

DESIGN
- [ ] Complete CSS token block written
- [ ] Both fonts confirmed (heading + body)
- [ ] Component rules noted (card, CTA, nav, inputs)
- [ ] Saved to docs/design-system.md
- [ ] Visual reference or prototype in docs/ (if exists)

USER FLOW AND SCREENS
- [ ] User flow written as numbered steps
- [ ] All screens listed with MVP / Phase 2 / Later tags
- [ ] Build order defined
- [ ] MVP is 6 screens or fewer

TECHNICAL
- [ ] GitHub repo exists
- [ ] Local folder path confirmed
- [ ] Live URL confirmed
- [ ] DNS location noted
- [ ] Vercel project noted
- [ ] All env vars in .env.example
- [ ] Supabase URL and region confirmed (if needed)
- [ ] Auth type confirmed (if needed)
- [ ] AI features and model confirmed (if needed)
- [ ] Node 20+, React 19, Vite 6, Tailwind v4 noted
- [ ] Tailwind v4 syntax note in CLAUDE.md
- [ ] Existing codebase noted (what's already built)

CONTENT AND DOCS
- [ ] docs/ folder created and populated
- [ ] Every docs/ file referenced by name in CLAUDE.md
- [ ] Content language and tone in CLAUDE.md

FILES
- [ ] CLAUDE.md — complete, no placeholders
- [ ] vercel.json — written
- [ ] .env.example — all keys
- [ ] .gitignore — written
- [ ] docs/ — all files present
- [ ] supabase/schema.sql (if needed)
- [ ] All files pushed to GitHub

---

## HANDOFF MESSAGE

"Ready. Here's what to do:

1. cd [local-folder-path]
2. git pull origin main  (or git clone [repo-url] if new)
3. npm install
4. cp .env.example .env.local — fill in every value
5. Open Claude Code Desktop → Open Project → [local-folder-path]
6. Paste this as your first message:

   Read CLAUDE.md fully. Read every file in docs/ before doing anything else.
   Enter plan mode. Show me a numbered build plan for all MVP screens.
   Flag any gaps, risks, or missing information.
   Do NOT write any code yet. Wait for my approval.

You're ready."

---

## HENRIK'S DEFAULTS

- GitHub org: 361Henrik
- Stack: React 19 + TypeScript strict + Vite 6 + Tailwind CSS v4 + Lucide + Framer Motion
- Deploy: Vercel, auto-deploy from main
- Domain: ask every session — never assume
- Database: Supabase if needed
- Auth: Supabase Auth if needed
- AI: Anthropic claude-sonnet-4-6 if needed
- Node: 20+
- Skills: /Users/henri/.claude/skills/
- No broken builds. Ever.
- Commit format: feat: / fix: / chore: / docs:
- Claude Code always enters plan mode first. Always waits for approval.
