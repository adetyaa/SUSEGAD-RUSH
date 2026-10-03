# GAME_SPEC: Susegad Rush

**Pitch:** A voice-controlled 3D endless runner through Goa. You are a builder racing the Demo Day clock. Susegad is the Goan "take it easy" attitude, and the joke is that you never get to.
**Tagline:** Run Goa. Ship fast. Susegad later.
**Context:** Entry for the Hacker House Goa "Wispr Flow" task. It is a fan-made game and must not claim to be official.

## 1. Core loop
- Three lanes. The runner moves forward automatically. Speed ramps up over time.
- Actions: left, right, jump, slide.
- Collect cashews (coins) and $HHG tokens. Dodge Goan obstacles. Survive as long as possible.
- You get one hit of grace: the first hit stumbles you and lets the Demo Day clock gain on you. A second hit within 8 seconds ends the run.
- Score = distance + coins x 10 + combo bonuses. High score is saved in localStorage.

## 2. Controls (all must work)
| Action | Voice (English) | Voice (Hindi) | Keyboard | Touch |
|---|---|---|---|---|
| Left | "left" | "baayein" | A / Left | swipe left |
| Right | "right" | "daayein" | D / Right | swipe right |
| Jump | "jump", "up" | "kood" | W / Up / Space | swipe up |
| Slide | "slide", "down" | "jhuko" | S / Down | swipe down |

Voice rules:
- Web Speech API, continuous with interim results, `lang = 'en-IN'`. Act on interim results for low latency.
- Match the last 1 to 2 words of the transcript. Allow fuzzy matches (edit distance up to 1). Add 250 ms debounce per command so one word never fires twice.
- Auto-restart recognition when it ends. Show a pulsing "MIC LIVE" badge. If unsupported or denied, show a clear message and switch to keyboard and touch.
- Hindi alternates are best-effort. Keep a visible on-screen cheat sheet for the first run.

## 3. Voice power words
Collecting $HHG tokens fills a "Hype" meter (3 segments). Spending a segment lets you say a power word.
| Word | Effect | Cost |
|---|---|---|
| "Ship it" | 5 s speed boost, invincible, score x2 | 2 segments |
| "Deploy" | Shield absorbs the next hit | 1 segment |
| "Hotfix" | Instantly pushes the Demo Day clock back | 1 segment |
| "Mint" | 6 s coin magnet | 1 segment |
Show the available words in the HUD, lit up only when affordable.

## 4. Volume = power
Use the mic level (AnalyserNode). Jump height scales from 0.8x (quiet) to 1.4x (loud) of the base jump. Show a small mic level bar in the HUD. Clamp and smooth the value so it never feels random.

## 5. Terminal gates (where Wispr Flow shines)
- About every 900 m a gate appears. Time slows to 30% and a terminal bar opens.
- It shows a phrase such as: `git push origin main`, `ship it to goa`, `npm run build`, `deploy to demo day`, `fix the bug`, `merge the pull request`.
- The player types it or dictates it with Wispr Flow into the focused text field. Case and punctuation are ignored. Tolerance: 85% similarity passes.
- Pass: +500 points, the gate opens, one free Hype segment. Fail or 6 s timeout: the clock gains on you.
- Show a hint line: "Press your Wispr Flow key and say the phrase." Do not detect Wispr Flow itself; any text input method works.

## 6. The chaser: Demo Day clock
A giant ring clock rolling behind the runner with a DEMO DAY countdown on it. It starts far away. Hits, failed gates and idling bring it closer. Power words and clean runs push it back. It touching the runner ends the run.

## 7. Characters (pick one on the menu)
| Builder | Perk |
|---|---|
| Dev | Tokens fill Hype 25% faster |
| Designer | Combo multiplier grows faster |
| Marketer | Coins worth 1.5x |
Build them procedurally with primitives and the palette. Each has a distinct outfit color and one accessory (laptop bag, beret, megaphone).

## 8. Zones
Change zone about every 600 m with a smooth sky and fog color blend. See `GOA_WORLD_AND_ASSETS.md` for contents. Order: Baga Beach Strip, Beach Run (waves), Fontainhas Streets, Paddy and Backwaters, Chapora Fort Road, Anjuna Night Market, then loop with a faster speed.

## 9. Difficulty
- Base speed 14 units/s rising to 30 over about 4 minutes.
- Obstacle density rises per zone loop.
- Never spawn an unavoidable pattern: always leave at least one safe lane or a jumpable or slideable option. Test this rule in code.

## 10. Game flow and screens
1. **Title:** big wordmark, play button, character pick, mic permission step, cheat sheet.
2. **Run:** HUD with score, coins, Hype meter, mic badge and level, zone name, clock distance bar.
3. **Pause:** says "pause" or press Esc.
4. **Game over:** run summary, best score, retry button, "Share card" button that draws a PNG on a canvas with the score.

## 11. Juice (small things that make it feel good)
Camera shake on hits, squash and stretch on jump and land, dust and sand particles, coin sparkle burst, speed lines during Ship it, slight camera FOV push when boosting, floating "+10" texts, zone title banner sliding in.

## 12. Audio (procedural Web Audio only)
Per-zone loop built from a kick, hat and simple pentatonic bass or arp. SFX: jump, slide, coin, token, hit, power word, gate pass and fail, wave swoosh (filtered noise). Master mute button. Start audio only after the first user gesture.

## 13. Out of scope
Multiplayer, backend, accounts, real-money crypto features. "$HHG" is a fictional in-game token only.
