# MASTER PROMPT: build "Susegad Rush"

You are a senior game developer and visual designer. Build a polished, Goa-themed 3D endless-runner for a hackathon, using only Three.js, HTML and CSS. Everything visual and audible must be generated in code (no external models, textures, images or audio files).

## Step 0: read before doing anything
Read these files completely, in order:
1. `docs/GAME_SPEC.md` (what the game is)
2. `docs/DESIGN_SYSTEM.md` (look and feel; also study the 4 attached screenshots of the Hacker House Goa website)
3. `docs/GOA_WORLD_AND_ASSETS.md` (zones, obstacles, procedural asset recipes)
4. `docs/TECH_PLAN.md` (architecture, voice system, milestones, performance rules)

## Step 1: short research (max 10 searches, then stop)
Search the web only for what changes the build. Save findings to `docs/RESEARCH_NOTES.md` (max 60 lines, bullet points, no copied text):
- Goa visual references: Baga/Calangute beach strip, Fontainhas colored houses, Old Goa churches, Chapora fort, Anjuna flea market, paddy fields, laterite roads.
- Three.js toon shading and inverted-hull outline technique that matches the flat, thick-outline illustration style of the screenshots.
- Endless-runner techniques: chunk pooling, lane logic, difficulty ramps, juice (camera shake, squash and stretch).
- Web Speech API in Chrome: interim results, restart-on-end behavior, mic permission flow, using it alongside an AnalyserNode.
Then reply with a plan of 10 lines or fewer, and start building. Do not wait for approval unless something in the docs contradicts itself.

## Step 2: build in milestones
Follow the milestones M0 to M7 in `docs/TECH_PLAN.md`, in order. After each milestone:
- Run the game locally and check the browser console is clean.
- Fix what is broken before moving on.
- Make one git commit with a clear message.
- Report in 3 lines or fewer what works and what is next.

## Hard rules
- Stack: vanilla ES modules, Three.js (pinned version, vendored locally if possible), plain CSS. No frameworks, no bundler required.
- No external assets. The only allowed external request is Google Fonts, and every font must have a fallback stack.
- Palette lock: every color in the game and UI comes from `DESIGN_SYSTEM.md`.
- Voice control must work with the keyboard and touch fallbacks always available.
- Performance target: 60 fps on a mid-range laptop, reasonable on a phone.
- Token discipline: send patches or changed functions, not whole files, unless a file is new. No long explanations. Do not reread files you already read unless they changed.
- Use English for all UI copy, with Hinglish voice command alternates as described in the spec.

## Definition of done
A person opens `index.html` through a local server, taps Start, grants the mic, and can play a full run by voice in Chrome. The game looks like a moving version of the Hacker House Goa website illustrations. It has at least 4 zones, 8 obstacle types, the power words, a terminal gate, the Demo Day chaser, a game-over screen and a README with run instructions.
