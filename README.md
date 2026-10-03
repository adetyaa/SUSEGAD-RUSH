# Susegad Rush

**Run Goa. Ship fast. Susegad later.**

A voice-controlled 3D endless runner through Goa, built for the Hacker House Goa × Wispr Flow task. Fan-made, not official. `$HHG` is a fictional in-game token.

▶ **Play:** https://adetyaa.github.io/SUSEGAD-RUSH/

## Run locally
The whole game is one file, `index.html` (Three.js loads from a CDN).

```bash
python -m http.server 8000
```
Then open http://localhost:8000 in Chrome. Voice needs localhost or https.

## Controls
| Action | Voice | Keys | Touch |
|---|---|---|---|
| Left / Right | "left" / "right" (baayein / daayein) | ← → or A D | swipe |
| Jump | "jump" (kood). Louder = higher | ↑, W, Space | swipe up |
| Slide | "slide" (jhuko) | ↓, S | swipe down |
| Pause | "pause" | Esc | ⏸ |

## Wispr Flow
The **WISPR FLOW** bar stays focused during a run. Hold your Wispr key, say a power word, release, and it fires. Press `/` to type a word by hand.

**Power words** (cost Hype): SURFBOARD, PARAGLIDER, SCOOTER, SHIP IT, DEPLOY, HOTFIX, MINT, COCONUT, CHAI. Keys 1–9 work too.
- Say two at once for a **voice combo**.
- **Terminal gates**: dictate the command shown. Every third gate is a long one, and each shows your words per minute.
- **Shout-outs**: "Goa!", "Susegad!", "Hacker House!".

## Features
- 8 zones across one Goan day: Baga, Beach Run, Fontainhas, Panjim Carnival, Monsoon Palm Roads, Mandovi Ferry, Chapora at sunset, Anjuna Night Market
- Demo Day clock chaser and a boss chase
- Rooftop running, moving traffic, daily missions, and a shop
- All models, textures, music and sound generated in code

Add `?debug` to the URL for a debug panel.

## Docs
Planning docs are in [`files/`](files/).
