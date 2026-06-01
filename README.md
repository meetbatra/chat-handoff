# chat-handoff

A Claude skill that automatically generates a handoff markdown file when your chat gets too long — so you can switch to a new chat without losing any context.

## What it does

When you tell Claude "this chat is getting too long" or "make a handoff file", the skill:

1. Reads the entire conversation automatically — no questions asked
2. Extracts everything: who you are, what's been done, what's pending, your schedule, deadlines, style preferences, flagged items
3. Generates a self-contained markdown file structured as a prompt for the next AI
4. The new chat picks up exactly where you left off — feels like a continuation, not a fresh start

## Who this is for

Anyone using claude.ai (or other AI chat interfaces) for long sessions — studying for exams, working on projects, research, planning, anything. This is **not** a Claude Code skill. It works in the regular chat interface.

## How it's different from other handoff skills

Every other handoff skill on GitHub is built for **Claude Code** — they work with git state, repositories, JSONL session files, and coding workflows.

This skill is built for **conversational chat sessions** — study sessions, project planning, research, work tasks. Any long conversation where you need to switch chats without losing your place.

## Installation

1. Download `SKILL.md` from this repo
2. In Claude.ai, go to **Settings → Skills → Install**
3. Upload the file

That's it. The skill is now available in all your future chats.

> Works with Claude Pro, Max, Team, Enterprise, and Free tiers.

## Usage

Just say it naturally in any chat:

- "This chat is getting too long, make a handoff"
- "Switch chat"
- "Create a markdown to continue in a new chat"
- "Too many tokens, handoff"

Claude generates the file immediately — no questions, no back and forth.

You can also pass extra context inline:

> "Make a handoff, also note that the deadline moved to June 25"

It'll incorporate that into the file automatically.

## What the output looks like

The generated `handoff.md` is structured as a briefing for the next AI:

```
1. WHO YOU ARE TALKING TO       — your background, communication style
2. WHAT THIS SESSION IS ABOUT   — goal, deadline driving it
3. CONTEXT & BACKGROUND         — domain-specific details
4. FULL PROGRESS STATUS         — every item, ✓ Done or ⬜ Pending
5. FLAGGED ITEMS                — things to revisit
6. SCHEDULE / DEADLINES         — dates, blocked days, day-by-day plan
7. WHERE TO PICK UP             — exact next step + opening line for new chat
8. STYLE / BEHAVIOUR INSTRUCTIONS — your preferences, things AI should not repeat
9. HARD CONSTRAINTS             — domain rules (if any)
```

Works with Claude, ChatGPT, Gemini, or any other AI — the output is plain markdown, no Claude-specific assumptions.

## Example use cases

- Studying for an exam across multiple days — tracks topics done, pending, schedule
- Long coding project — tracks decisions made, files changed, what's next
- Research session — tracks sources used, angle, open questions
- Work planning — tracks tasks, stakeholders, decisions

## Repo structure

```
chat-handoff/
└── SKILL.md    # The skill file — this is all you need to install
README.md
```

## License

MIT
