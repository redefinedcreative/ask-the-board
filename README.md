# Ask the Board

A Claude skill that convenes your personal Board of Advisors on any decision. Each advisor answers in their own voice, you see where they agree and clash, and you get one clear call plus a next step tuned to your goals and failure modes.

The skill is the framework. **Your board is separate**, so you can run different boards in different parts of life (business, day job, personal) and share the skill without sharing your board.

## Install

Clone straight into Claude's skills folder. No symlinks are needed, which also works on locked-down work machines.

**macOS / Linux**
```bash
git clone https://github.com/redefinedcreative/ask-the-board.git ~/.claude/skills/ask-the-board
```

**Windows (PowerShell)**
```powershell
git clone https://github.com/redefinedcreative/ask-the-board.git "$env:USERPROFILE\.claude\skills\ask-the-board"
```

To update later, run `git pull` inside that folder.

Then say **"build my board"** in Claude Code. It interviews you and creates `~/.claude/boards/<name>/`. Or copy `templates/` by hand:

```
~/.claude/boards/<name>/
  board.md            seats: who sits, what they're for
  profile.md          you: goals, failure modes, how you want to be coached
  advisors/<slug>.md  one file per advisor
  sources/            optional raw notes
```

A board folder can be a symlink, so it can live in any repo you already back up.

## Use

- "Ask the board: should I take this client at a discount?"
- "Ask the work board whether to push the migration to Q2."
- "Add Cal Newport to my board."

If you have one board, it's used automatically. If you have several, name the one you want, or the skill will ask.

## Packaging

The skill folder contains no personal data. Boards live outside it. To share or sell, ship this folder as-is. A license still needs to be chosen before publishing.
