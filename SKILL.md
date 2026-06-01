---
name: chat-handoff
description: Generate a handoff markdown file so the user can continue a long conversation in a new chat without losing any context. Use this skill whenever the user says things like "this chat is getting too long", "switch chat", "new chat", "handoff", "create a markdown to continue", "context is getting large", "too many tokens", "make a handoff file", or any variation of wanting to move the current work session to a fresh conversation. Works for any context — studying, coding projects, research, work tasks, planning, or anything else. Trigger immediately when the user asks, no clarifying questions needed unless they explicitly add extra instructions alongside the request.
---

# Chat Handoff Skill

Generate a self-contained markdown file that lets any AI (Claude or otherwise) continue the current session seamlessly — as if no chat switch happened.

---

## Core Principle

Extract everything from the conversation. Ask the user nothing unless they explicitly give you extra instructions alongside the handoff request (e.g. "make a handoff, also note that the exam date changed to June 20"). If they say something like that, incorporate it. Otherwise, read the conversation and infer everything yourself.

---

## Step 1 — Read the Conversation Thoroughly

Before writing anything, scan the entire conversation for:

- **What is this session about?** (studying, project, research, work task, planning, etc.)
- **Who is the user?** Any identity context mentioned (name, role, school, company, tools they use, background)
- **What has been completed?** Every topic covered, problem solved, task done, decision made
- **What is pending?** Everything mentioned but not yet done
- **What schedule or deadlines exist?** Dates, exam days, blocked days, milestones
- **What style preferences did the user express?** Teaching style, communication preferences, rules for the AI to follow, things they explicitly asked for or pushed back on
- **What was flagged for later?** Problems to revisit, things the user said were tricky, open questions
- **What is the very next thing to do?** The exact point where this chat ended

---

## Step 2 — Write the Handoff File

Output a single markdown file to `/mnt/user-data/outputs/handoff.md`.

Structure it as a prompt for the next AI agent — written in second person ("You are talking to..."), as if briefing a new agent who has never seen this conversation.

### Required Sections (adapt names/content to context):

---

### 1. WHO YOU ARE TALKING TO
One paragraph. Name, role/background, relevant tools or experience, communication style (e.g. "direct, no flattery, wants blunt feedback").

---

### 2. WHAT THIS SESSION IS ABOUT
One paragraph. What are they working on? What's the goal? What event/deadline is driving this (exam, launch, submission, etc.)?

---

### 3. CONTEXT & BACKGROUND
Any domain-specific details the next AI needs to know upfront. For example:
- For a placement prep: the company, role, interview rounds, platform, constraints
- For a coding project: the stack, architecture decisions made, constraints
- For research: the topic, angle, what sources have been used
- For work: the task, stakeholders, decisions already made

Keep it factual and dense — no fluff.

---

### 4. FULL PROGRESS STATUS
A complete, scannable status table or list. Every item that was planned — mark it ✓ Done or ⬜ Pending. Be exhaustive. Group logically (by topic, module, feature, etc.).

Include sub-details where relevant (e.g. which approach was used, what constraint applies, if it was flagged for revision).

---

### 5. FLAGGED ITEMS
Anything the user explicitly said was tricky, confusing, needs revisiting, or should be noted for later. Even one item deserves its own section.

---

### 6. SCHEDULE / DEADLINES
If any dates, timelines, or blocked periods were mentioned — list them clearly. Include:
- The deadline or event date
- Blocked/unavailable days
- Remaining available days
- Day-by-day plan if one exists

---

### 7. WHERE TO PICK UP
One clear, unambiguous statement: what is the very next thing to do? Be specific — not "continue studying" but "Start with CSS Animations, then move to LC 658."

Also include what to say as the opening line of the new chat (e.g. "Say: 'Hey [name], picking up right where we left off. Today is [date] — let's get into it.'")

---

### 8. STYLE / BEHAVIOUR INSTRUCTIONS
Any rules the user set for how the AI should behave. This is critical — if the user pushed back on something, corrected the AI, or stated a preference, capture it here so the next AI doesn't repeat the mistake.

Examples:
- "When the user challenges your reasoning, verify before pushing back — they have been right multiple times"
- "Don't give unsolicited encouragement or flattery"
- "Teach 4-5 topics at a time, then give a copy-pasteable example"
- "One topic at a time. Don't dump everything at once"
- "If code is correct, confirm and move on — don't over-explain"

---

### 9. HARD CONSTRAINTS (if applicable)
Domain-specific rules that must always be followed. E.g.:
- No built-in data structures
- Vanilla HTML/CSS/JS only
- No external libraries
- Specific file structure requirements

Only include this section if hard constraints exist.

---

## Step 3 — Filename and Delivery

Save to: `/mnt/user-data/outputs/handoff.md`

If a handoff file already exists from this session (user is doing a second switch), name it `handoff_v2.md`, `handoff_v3.md`, etc.

Then call `present_files` with the path so the user can download it immediately.

---

## Writing Rules

- Write for **any AI reader**, not just Claude. Use plain language, no Claude-specific assumptions.
- Be **dense and specific**, not generic. "CSS Grid — all 12 topics done" is good. "CSS mostly done" is useless.
- **Never summarize vaguely**. If something was covered, say exactly what was covered.
- **Tense**: Write the status sections in present tense ("X is done", "Y is pending").
- **Opening line of new chat**: Always include a suggested first message for the new AI to say — this kills the "new chat" feeling immediately.
- **Date awareness**: Use the actual current date when writing the schedule and "where to pick up" sections.
- Keep the file **self-contained** — the next AI should need nothing else to continue.

---

## What NOT to Do

- Do not ask the user questions before generating (unless they gave you extra instructions in the same message)
- Do not include meta-commentary like "I've summarized the session below"
- Do not truncate the progress table — every item must appear
- Do not write in first person ("I covered X") — write as a briefing ("X has been covered")
- Do not forget flagged items — these are often the most important things to carry forward
