Code prep assistant — Henrik's foundational pre-flight before any Claude Code session. Use this skill at the start of any new build session. Trigger phrases: "start a new project", "get ready to code", "set up the project", "prep for Claude Code", "create CLAUDE.md", "build this", "I want to build", "new project setup", or any time a new coding session begins. Project-neutral — runs the same way every time for every project.

# CODE PREP ASSISTANT
## Henrik Host / ThreeSixtyOne — Foundational Build Instantiation

This skill is project-neutral. It runs the same way every time, for any project type:
client work, own products, new ideas, quick tools, prototypes — all of them.

---

## WHAT IT COLLECTS

- What we're building and why (brief / PRD)
- Tech stack, auth, database, hosting
- Design system and exact brand tokens
- Environment variables and services needed
- Content sources and local reference files
- The exact build order and instruction for Claude Code

The output is a fully loaded local project folder.
Claude Code opens it cold and enters plan mode immediately.
No back and forth. No explaining context. No guessing.

---

## BEFORE THE CHECKPOINTS — ASK FOR DOCUMENTS

Before running any checkpoint, always ask:
"Do you have anything to share? A brief, PRD, design file, screenshot, reference doc, or upload?
Drop it here first and I'll read it before we start."

Anything shared goes into `docs/` in the local project folder so Claude Code can reference it directly.
This includes: uploaded PDFs, Google Doc links, Notion pages, screenshots, design files, content drafts, brand guides, anything.

---

## HOW IT RUNS

Work through 8 checkpoints in order.
For each: ask if it's already done.
- YES — take it, move on
- NO — ask ONE targeted question to fill the gap. Never more than one at a time.

Target: done in under 10 minutes.

---

## CHECKPOINT 1 — THE BRIEF

Ask: "Do you have a brief, PRD, or description of what we're building?"

- YES — take it (paste, doc link, or summary). Extract: what it does, who it's for, core purpose.
- NO — ask: "Give me the idea in 2-3 sentences." Structure into a one-paragraph brief.

Capture: project name, one-sentence purpose, intended audience.

---

## CHECKPOINT 2 — CLARITY

Ask: "Is the purpose, audience, and scope clear enough to start building?"

- YES — move on.
- NO — ask the ONE most important missing question. Capture the answer. Move on.

One question maximum.

---

## CHECKPOINT 3 — RESEARCH

Ask: "Does this need market or feasibility research before we start?"

- YES — run the research-gate skill, return here with findings.
- NO — skip entirely.

Most projects skip this.

---

## CHECKPOINT 4 — PRIORITY

Ask: "Is this the right thing to build right now?"

- YES — move on.
- NOT SURE — quick score: real problem? feasible? fits current focus?
  Rate HIGH / MEDIUM / LOW. Confirm before continuing.

---

## CHECKPOINT 5 — USER FLOW

Ask: "Do you have a user flow or journey map for this?"

- YES — take it. Summarise the key steps.
- NO — ask: "Who uses this? What's the first thing they do? What's the outcome?"
  Build a 5-step flow from the answers.

Capture: core user journey as numbered list.

---

## CHECKPOINT 6 — SCREENS AND FEATURES

Ask: "Do you know what screens or features this needs?"

- YES — take the list.
- NO — derive from the user flow. List implied screens. Confirm: "Does this cover it?"

Capture: numbered list of screens/sections in intended build order.

---

## CHECKPOINT 7 — VISUAL REFERENCE

Ask: "Do you have a mockup, prototype, screenshot, or visual direction?"

- YES — note the reference. Ask: "Should I build a clickable prototype first, or go straight to Claude Code?"
- NO — ask: "Which design system applies to this project?"
  Collect the exact tokens, fonts, and brand rules now.
  If it's an own product: use ATLASdesign tokens.
  If it's a client project: collect their brand system.
  If it's new: note it — define during build.

Always offer: "Want me to generate a visual prototype before we hand off to Claude Code?"

Capture: design system name + complete token set + any visual reference.

---

## CHECKPOINT 8 — TECHNICAL SETUP

Always runs fully. Ask each item only if not already known.

### 8a. Repo
"What is the GitHub repo name?"
Format: 361Henrik/repo-name
If it doesn't exist: offer to create it via GitHub connector.

### 8b. Local folder
"What is the local folder path on your Mac?"
Common locations: ~/Developer_ClaudeCode/ or ~/Developer/active/

### 8c. Live URL
"What is the target live URL?"
Could be any domain — ask, never assume.
DNS may be in Squarespace, Vercel, or a client's domain manager.

### 8d. Auth
"Does this need user authentication / secure sign-in?"
- YES — Supabase Auth. Env vars: VITE_SUPABASE_URL + VITE_SUPABASE_ANON_KEY
- NO — skip

### 8e. Database
"Does this need a database?"
- YES — Supabase (PostgreSQL). Existing project or create new?
  Schema SQL goes in supabase/schema.sql
- NO — skip

### 8f. AI features
"Does this need AI features — chat, generation, analysis, Claude API?"
- YES — which features? Env var: VITE_ANTHROPIC_API_KEY. Model: claude-sonnet-4-20250514
- NO — skip

### 8g. Other services
"Any other services? Stripe, email, storage, third-party APIs?"
Note each with its required env var name.

### 8h. Design tokens
Write the complete token block based on what was confirmed in Checkpoint 7.
ATLASdesign tokens are stored in this skill for Henrik's own products.
For client or new projects: use exactly the values collected in Checkpoint 7.

ATLASdesign (Henrik's own products):
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

For any other project: collect exact hex values and font names during Checkpoint 7 and write the equivalent block.

---

## OUTPUT — CREATE THESE FILES

Once all 8 checkpoints are complete, produce the following.
Push to GitHub. Confirm each file before moving on.

### FILE 1: CLAUDE.md (project root)

```markdown
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

- [ ] npm install — no errors
- [ ] .env.local exists with all values filled in
- [ ] npm run dev — loads on localhost:3000
- [ ] npm run build — no TypeScript errors

---

## PROJECT

**What it is:** [one sentence]
**Core purpose:** [why it exists]
**Audience:** [who uses this]
**Key outcome:** [what users should think, feel, or do]

---

## DESIGN SYSTEM

[Full @import and @theme block from Checkpoint 8h]
[Typography rules]

---

## USER FLOW

[5-step numbered flow from Checkpoint 5]

---

## SCREENS / SECTIONS TO BUILD

[Numbered list in build order from Checkpoint 6]

---

## BUILD ORDER

1. src/index.css — full design token replacement
2. src/App.tsx — shell and navigation
3. [Each screen/section in order]
Final: npm run build → fix errors → commit → push to main

---

## ENVIRONMENT VARIABLES

VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=
VITE_ANTHROPIC_API_KEY=
[any others from Checkpoint 8g]

---

## CONTENT SOURCE

[Where content comes from]
[If docs/ folder has files — list them here and instruct Claude Code to read them before building]

---

## THE ASK

> Read CLAUDE.md fully. Read all files in docs/ if they exist.
> Enter plan mode. Show me a numbered build plan.
> Flag any gaps or risks in the current codebase.
> Do NOT write any code yet. Wait for my approval.
```

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

### FILE 5: docs/ folder
Create this folder and populate it with any documents Henrik shared at the start of the session.
Name files clearly: `brief.md`, `content.md`, `brand-guide.md`, `user-research.md`, etc.
Claude Code reads everything in docs/ before writing a single line.

### FILE 6: supabase/schema.sql
Only if database is needed. Write initial schema from the brief.

---

## HANDOFF MESSAGE

After all files are ready:

"Ready. Here's what to do:

1. cd [local-folder-path]
2. git pull origin main  (or git clone [repo-url] if new)
3. npm install
4. cp .env.example .env.local — fill in the values
5. Open Claude Code Desktop → Open Project → [local-folder-path]
6. Paste this as your first message:

   Read CLAUDE.md fully. Read all files in docs/ if they exist.
   Enter plan mode. Show me a numbered build plan.
   Do NOT write any code yet. Wait for my approval.

You're ready."

---

## HENRIK'S DEFAULTS

- GitHub org: 361Henrik
- Stack: React 19 + TypeScript + Vite 6 + Tailwind CSS v4 + Lucide + Framer Motion
- Deploy: Vercel, auto-deploy from main branch
- Domain: ask every time — could be any domain
- Database: Supabase if needed
- AI: Anthropic Claude API if needed
- Auth: Supabase Auth if needed
- Skills folder: /Users/henri/.claude/skills/
- No broken builds. Ever.
- Commit format: feat: / fix: / chore: / docs:
