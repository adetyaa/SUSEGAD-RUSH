# START HERE: how to use these files

## What to give Opus 5.5
Create a new project folder and put these in it:
```
susegad-rush/
  PROMPT_FOR_OPUS.md        <- the master prompt (Opus reads this first)
  docs/
    GAME_SPEC.md
    DESIGN_SYSTEM.md
    GOA_WORLD_AND_ASSETS.md
    TECH_PLAN.md
    SUBMISSION_AND_DEMO.md  <- for you, Opus does not need it
  reference/
    (your 4 Hacker House Goa screenshots)
```
Rename the screenshots to `hhg-1-days.png`, `hhg-2-signpost.png`, `hhg-3-task-card.png`, `hhg-4-hero.png`.

## How to start (keep it voice-driven)
1. Open the folder in Claude Code (or attach the files in a Claude chat if you use the web app).
2. If you use chat, attach all the files and the 4 screenshots in the first message.
3. Say to Wispr Flow: "Read PROMPT_FOR_OPUS.md and follow it. The screenshots are in the reference folder."
4. After each milestone, say: "Looks good, continue to the next milestone." or describe what to fix.

## Saving your Pro credits
- Skip `SUBMISSION_AND_DEMO.md` when attaching files to Opus (it is for you).
- Keep one milestone per turn and ask for patches, not whole-file rewrites.
- Use a lighter model for small CSS and text fixes if your plan allows it.
- Start a fresh chat after a few milestones and say "Read docs/TECH_PLAN.md and continue from milestone M4." Do not re-upload everything.
- Do not keep dictating long rambling messages. Short and specific uses fewer tokens.

## Order of work
Read `PROMPT_FOR_OPUS.md` first, then the docs, then follow the milestones M0 to M7 in `docs/TECH_PLAN.md`. Submit before Oct 6, 11:59 PM using `docs/SUBMISSION_AND_DEMO.md`.
