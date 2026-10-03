# DESIGN_SYSTEM: match the Hacker House Goa site

Study the 4 attached screenshots. The game must feel like the website's illustration world come to life in 3D, and the UI must feel like the same site. Hex values below were estimated by eye from the screenshots; if the screenshots show something different, the screenshots win.

## 1. Visual identity in one line
Flat, bold, sunny Goa poster art: limited palette, thick dark outlines, white wave and sun-ray line work, hanging signboards, beach shacks and palms.

## 2. Palette (lock it)
| Token | Hex | Use |
|---|---|---|
| `--forest` | `#046A38` | page and menu background, deep scenery |
| `--leaf` | `#11A860` | bright foliage, sky tint, illustration green |
| `--sun` | `#FFE600` | primary accent, headlines, sun disc, buttons |
| `--hype-pink` | `#F0149F` | secondary accent, highlights, hazards you must notice |
| `--cream` | `#FFF8E1` | cards, panels, light surfaces |
| `--ink` | `#0B3B2A` | outlines, text on cream, shadows |
| `--tile` | `#E8683A` | terracotta roofs, warm props |
| `--foam` | `#FFFFFF` | waves, rope, line work, sand highlights |
| `--card-shadow` | `#064D2A` | hard offset shadows under cards |
Rule: no colors outside this table, except tints and shades of these (for example a darker `--forest` at night). Night zone uses deep `--forest` and `--ink` sky with `--sun` and `--hype-pink` neon accents.

## 3. Typography
- **Display (headlines, wordmark, big numbers):** a tall, condensed, high-contrast serif in all caps, like the "HACKER HOUSE" headline in the screenshots. Pick the closest free Google Font after comparing options (try Bodoni Moda, Gloock, Playfair Display SC), and use `transform: scaleX(0.8)` or letter-spacing tweaks if needed to get the tall condensed feel. Fallback: `'Times New Roman', serif`.
- **Body and labels:** a monospace face (try Space Mono or Courier Prime), as in "DAY 01 - GENESIS DAY" and the task card text. Fallback: `ui-monospace, monospace`.
- Small pink labels such as "TASK #2" are used for category tags. Use bullets as pink sparkles (✦).
- Use one more playful touch only: the Devanagari word "गोवा" in pink as a sticker over the wordmark, like the site (use a bold Devanagari font such as Hind or Mukta, fallback sans-serif).
- Do not copy the 2:47PM Studio logo. Make our own wordmark: SUSEGAD RUSH in the display font, with a pink "गोवा" sticker.

## 4. UI components (copy the site's patterns)
- **Hanging signboards:** rectangular boards hanging from two ropes, thick outer color (yellow or pink), inner white inset border, mono text inside. Use for the title menu items, zone banners and the pause screen.
- **Direction signpost:** a white wooden post with arrow-shaped boards (yellow pointing left, pink pointing right) holding big numbers with small labels. Use for the HUD stats and the game-over summary.
- **Cards:** cream background, 12px radius, hard offset shadow (about 8px right and 10px down) in `--card-shadow`. Use for the character select and instructions.
- **Primary button:** yellow with ink display text, and a dotted or zigzag pink ribbon border like the site's APPLY button.
- **Message boxes:** pink-tinted background, pink border, red-pink mono text (for errors such as "MIC BLOCKED").
- **Backgrounds:** deep green with subtle film grain, a half sun with thin yellow ray lines rising at the bottom, palm silhouettes in the corners.
- **Motion in UI:** only answer user actions (button press, panel open). One orchestrated intro on load (wordmark drops in, sun rises). No scattered hover effects.

## 5. 3D art direction (the important part)
Goal: look like the flat illustrations, in motion.
- **Shading:** `MeshToonMaterial` with a 3-step gradient map, or flat `MeshBasicMaterial` for distant props. No realistic PBR.
- **Outlines:** inverted-hull outline on every main prop (back-face copy scaled slightly, color `--ink`). Thickness scales with distance if cheap to do.
- **Lighting:** one warm directional sun plus a hemisphere light. No shadow maps. Use simple blob shadows (dark transparent discs) under characters and obstacles.
- **Sky:** gradient sky dome plus a big flat `--sun` disc low on the horizon with thin ray lines. Seagull shapes (white V strokes) drifting across.
- **Fog:** green-tinted fog (`--leaf` to `--forest`) hides spawn pop-in and unifies the look.
- **Water:** flat `--leaf` or teal-tinted water with white wave lines scrolling (canvas-drawn texture, animated offset). Foam edge on the sand.
- **Sand and road:** warm white sand, red laterite road (`--tile` darkened), painted lane markers in `--sun`.
- **Palms:** outlined trunk with curved segments, big flat fronds with white highlight lines, as in the screenshots.
- **Houses:** white walls, terracotta tile roofs, shutters in pink and yellow (like the house in the first screenshot).
- **Props to reuse from the screenshots:** pink Vespa-style scooter, striped yellow and pink beach umbrella, green deck chairs, dark sailboat, signpost, chai cup, tender coconut.
- **Camera:** third person behind and above, slight lag, FOV 60 that eases to 68 on boosts.

## 6. Tone of voice (copy)
Short, funny, builder slang mixed with Goa: "Ship or ship." "Heads down." "Susegad later." Errors are plain and say what to do ("Mic blocked. Allow it in the address bar, or use the keyboard.").

## 7. Quality floor
Responsive from phone to desktop, visible keyboard focus, `prefers-reduced-motion` respected (turn off camera shake and parallax), readable contrast (yellow on forest, ink on cream), mute button always visible.
