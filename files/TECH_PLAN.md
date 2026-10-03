# TECH_PLAN

## 1. Stack
- Vanilla ES modules, Three.js (pinned version; vendor `three.module.min.js` into `/vendor` with npm at the start, and fall back to a pinned CDN `importmap` if that fails), plain CSS.
- Run with a local static server (`python -m http.server 8000` or `npx serve`). Chrome is the target browser because of the Web Speech API.
- Deployable as static files (GitHub Pages) with no build step.

## 2. File structure
```
index.html
css/style.css
js/main.js        // boot, state machine (title, run, pause, over)
js/config.js      // constants, palette, tuning numbers
js/game.js        // loop, speed, score, collisions, combo, difficulty
js/world.js       // chunk pool, spawner, zones, sky and fog blending
js/zones.js       // zone definitions, scenery placement
js/assets.js      // all procedural builders (props, obstacles, characters, clock)
js/textures.js    // canvas texture generators
js/player.js      // lanes, jump, slide, animation, stumble
js/voice.js       // speech recognition, command matching, mic level
js/powers.js      // hype meter, power words, terminal gates
js/audio.js       // procedural music and SFX
js/ui.js          // HUD, menus, banners, share card
docs/             // these files
README.md
```

## 3. Voice system details
- `SpeechRecognition` (or `webkitSpeechRecognition`), `continuous = true`, `interimResults = true`, `lang = 'en-IN'`, restart in `onend` unless the game is paused or stopped.
- Command table with synonyms (English and Hindi, see the spec). Normalize text (lowercase, strip punctuation). Use only the last 2 words of each interim result. Fuzzy match with edit distance up to 1. Per-command debounce of 250 ms and a short global lock after a successful command so interim updates don't repeat it.
- Mic level: `getUserMedia({audio:true})` into an `AnalyserNode`, smoothed RMS mapped to 0 to 1.
- Expose events: `onCommand(name)`, `onPowerWord(name)`, `onLevel(value)`, `onStatus(state)`.
- Terminal gate uses a normal `<input>` that auto-focuses, so any dictation tool (Wispr Flow) can type into it. Add Enter to submit and auto-submit on a 85% match.
- Handle: unsupported browser, denied permission, no mic found, network error from the recognizer (show a clear message and keep the fallbacks live).

## 4. Rendering and performance
- `WebGLRenderer({antialias:true})`, pixel ratio capped at 2, tone mapping off for a flat look.
- Instanced meshes for repeated scenery (palms, fence posts, lights). Share geometries and materials. Pool all obstacles, coins and chunks.
- No shadow maps (blob shadows only). Keep draw calls under about 250.
- Fixed-step update with a delta clamp. Pause when the tab is hidden.
- Provide a low-quality switch (fewer props, no outlines on far objects) if the frame rate drops under 45 fps for 3 seconds.

## 5. Collision
Use simple AABB boxes per obstacle and player, with forgiving shrink (about 10%). Slide shrinks the player's height box, jump lifts it. Grace hit rule from the spec.

## 6. Milestones (commit after each)
| M | Goal | Done when |
|---|---|---|
| M0 | Project skeleton, vendored Three.js, palette tokens, render loop, toon material and outline helper | A colored toon cube with outline spins on a sky-gradient background |
| M1 | Player, 3 lanes, jump, slide, keyboard and touch, chunk road, camera | You can run endlessly on a plain road |
| M2 | Voice control: commands, mic badge, mic level, fallbacks | Saying left, right, jump and slide moves the player reliably |
| M3 | Obstacles, collisions, coins, score, grace hit, game over | A full run is playable and fair |
| M4 | Zones 1 to 3 with full scenery, sky, fog, sea and wave texture | Baga, Beach Run and Fontainhas look like the website illustrations |
| M5 | Hype meter, power words, terminal gates, Demo Day clock | All power words and gates work, the chaser threatens the player |
| M6 | Zones 4 to 6, night market, loop speed-up, audio, juice | A 5-minute run feels varied and alive |
| M7 | Menus and HUD in the website style, character select, share card, README, polish pass | Looks consistent with `DESIGN_SYSTEM.md`, no console errors, README finished |
Cut order if time runs out: zone 6 variations, character perks, share card, extra obstacles. Never cut M0 to M5.

## 7. Testing (cheap but required)
- After each milestone: load the page, check for console errors, play for 60 seconds.
- Add a hidden `?debug` flag: shows fps, speed, zone, obstacle count, and lets you jump to any zone and spawn any obstacle.
- Unit-check the pattern generator: simulate 1000 chunks and assert a safe path always exists.
- If screenshots are possible (for example Playwright), take one per zone and compare to the design system.

## 8. Token discipline for the builder
- One milestone per focused turn. Send patches or changed functions, not whole files.
- Do not paste large files back into the chat. Do not reread docs unless they changed.
- Keep status reports to 3 lines.
- Put tuning numbers in `config.js` so tweaks are one-line edits.
