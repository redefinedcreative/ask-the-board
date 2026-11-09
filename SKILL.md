---
name: ask-the-board
description: >-
  Convene a personal Board of Advisors on a decision. Each advisor answers in their own
  voice, the skill names where they agree and clash, then gives one blunt recommendation
  and a next step tuned to the person's goals and failure modes. Works with any board:
  boards live in ~/.claude/boards/<name>/. Use when someone is weighing a choice,
  stuck on a call, asks "what should I do about X", debates a tradeoff, or says "ask the
  board", "convene the board", "what would the board say", "ask the <name> board", or
  "/ask-the-board". Also use to set up a new board or add an advisor ("build my board",
  "add <person> to the board").
---

# Ask the Board

A decision tool, not an essay. Surface real disagreement, then force a decision. A wishy-washy "it depends" fails the user.

This skill is the **framework**. Who sits on the board, whose goals it serves, and how it should coach all live in a **board folder**, so one skill serves any number of boards (work, business, personal) and can be shared.

## Step 0: Find the board

Boards live in `~/.claude/boards/<board-name>/`. Each folder can be a symlink to wherever the board is kept.

1. If the user names a board ("ask the work board"), use `~/.claude/boards/<that name>/`.
2. Otherwise, if exactly one board exists, use it.
3. If several exist and the request doesn't make it obvious, ask which board, in one line, listing their names.
4. If none exist, offer to build one (see **Building a board**).

A board folder contains:

| File | What it holds |
|---|---|
| `board.md` | The board's name, who it serves, the seats (advisor, seat, domain, file), when to seat each one, and synthesis rules |
| `profile.md` | The person the board serves: goals, constraints, how they want to be coached, failure modes. **Governs the synthesis.** |
| `advisors/<slug>.md` | One file per advisor: core ideas, signature vocabulary, stances, voice anchors, and "how to use this seat" |
| `sources/` | Optional raw notes behind the advisor files |

Read `board.md`, `profile.md` and the seated advisors' files **every time**. They change, and the files override anything remembered. If something is missing, say so in one line and continue with what's there.

## Step 1: Decide who has a seat at THIS table

Use the seat descriptions in `board.md`. Convene the **3–5** advisors whose domain actually bears on the decision. Convening everyone on a question only two can speak to is noise. If a major advisor is deliberately benched, give one line on why.

Some boards define **internal advisors**: real people from the user's life, such as a boss or a partner, voiced from what `board.md` and `profile.md` say about them. Label their takes "(inferred)" and keep them grounded in those files. Seat them only when `board.md` says they're relevant.

## Step 2: Each advisor's take, in their own voice

For each seated advisor, write a short take of about 3–6 sentences, first person, using their cadence and vocabulary. Their advisor file carries the signature terms, stories and voice anchors; use them so the voice is recognizable, not generic. Each advisor takes an actual **position** on this specific question. If they'd push back on the premise, let them.

## Step 3: Agreement and disagreement

- **Where they converge:** the through-line most of them share. This is usually the strong signal.
- **Where they genuinely clash:** the real tension, named as a tradeoff. If they all agree, say so, and note that consensus is a signal or a blind spot.

Don't manufacture conflict, and don't paper over it.

## Step 4: What to actually do

Coach in the style `profile.md` asks for. If it says nothing, be direct.

1. **The call.** One clear recommendation, stated first.
2. **Why**, in 2–3 tight sentences, leaning on the advisors who carried the strongest case.
3. **Failure-mode check.** Compare the decision, and the user's evident excitement about it, with the failure modes in `profile.md`. If it matches one, name it and redirect toward the goals in `profile.md`. If it's clear, say so.
4. **This week:** the smallest concrete next action.

If you can't recommend without one missing fact, ask exactly one sharp question. Don't hide behind "it depends."

## Output

```
## 🪑 The <Board name> on: [the decision in one line]

**[Advisor]** — *[seat]*
[take, first person, in voice]

… (3–5 advisors)

---

### Where they agree
[through-line]

### Where they disagree
[the real tension as a tradeoff]

---

### 🎯 What you should actually do
**The call:** …
**Why:** …
**Failure-mode check:** …
**This week:** …
```

Conversational, sharp, no filler. The takes should read as distinct people. Keep it to a screen or two; when in doubt, cut.

## Building a board

When the user wants a new board, or no board exists:

1. Ask for: the board's name and purpose (for example "business", "work", "life"); the person it serves; 3–7 advisors (public figures, authors, or people in their life); and how they want to be coached.
2. Create `~/.claude/boards/<name>/` from the templates in this skill's `templates/` folder: `board.md`, `profile.md`, and `advisors/<slug>.md` for each advisor.
3. For each public advisor, build their file from sources the user provides (talks, books, articles) or from research. Write a synthesis in your own words, never long quotations. Record the sources in `sources/<slug>/00-sources.md`.
4. For internal advisors, fill their file from the user's description only, and mark it "inferred".
5. Show the user the seat table and ask them to confirm or adjust it.

**Adding an advisor:** create `advisors/<slug>.md` from the template, add a row to `board.md`, and confirm.
