# GOA_WORLD_AND_ASSETS

Everything below is built in code from primitives (boxes, cylinders, cones, spheres, planes, extrusions) and canvas-generated textures. Use the palette in `DESIGN_SYSTEM.md`. Verify the real-world look of each place during your research step and adjust props to match.

## 1. Zones (about 600 m each)
| # | Zone | Look | Scenery | Zone-specific obstacles |
|---|---|---|---|---|
| 1 | **Baga Beach Strip** | Golden-hour sky, sun disc, green sea on the left | Palms, beach shacks with colored shutters, sun loungers, umbrellas, sailboat, seagulls | Scooters, tourists with selfie sticks, loungers |
| 2 | **Beach Run** | Run on wet sand, sea closes in on the left | Foam line, shells, boats pulled up on sand, fishermen's nets | Incoming waves (cover 1 to 2 lanes, with a 1 s warning shimmer), crabs, fishing nets |
| 3 | **Fontainhas Streets** | Narrow colorful lane, warm afternoon | Portuguese-style houses in pink, yellow, blue and white, balconies, a white church with steps at the end, laundry lines | Stray cows crossing, parked scooters, hanging laundry (slide under) |
| 4 | **Paddy and Backwaters** | Bright green fields, water channels, mild haze | Paddy strips, coconut palms, a small bridge, ducks, a wooden boat | Falling coconuts, bridge rails, ducks crossing |
| 5 | **Chapora Fort Road** | Late golden light, laterite red road, cliffs | Fort wall blocks, cliff edge with the sea, cashew trees, distant ramparts | Potholes, buses, fallen branches (jump) |
| 6 | **Anjuna Night Market** | Night, deep forest sky, neon pink and yellow | Fairy-light strings, striped market stalls, lanterns, a neon HACKER HOUSE sign, a DJ stage glow | Stall crates, crowds blocks, low string lights (slide) |
Loop to zone 1 with a faster pace and a new sky tint.

## 2. Obstacles (at least 8 unique types)
Each one has a clear silhouette, a clear action (dodge, jump or slide), and a hitbox simpler than its mesh.
| Obstacle | Action | Build recipe |
|---|---|---|
| Scooter (pink Vespa style) | change lane | rounded body from boxes and a sphere, 2 cylinder wheels, handlebar, round headlight; pink with cream seat |
| Stray cow | change lane or jump if lying | white and brown boxes, horns as small cones, tail, slow sideways walk |
| Bus (yellow and red) | change lane | long box, window strip, wheels, roof rack; wide, blocks 1 lane |
| Tourist with selfie stick | change lane | capsule body, bright shirt, hat cone, thin cylinder stick raised high |
| Sun lounger and umbrella | jump over lounger | flat box with slanted back, striped umbrella above (do not block the slide space) |
| Crab | jump | flattened sphere, 2 claws, 6 small legs, sideways scuttle |
| Fishing net on poles | slide under | two poles and a net plane with a canvas grid texture, bottom edge raised |
| Pothole | jump or lane change | dark ink ring decal with an inner shade, small rim |
| Falling coconut | lane dodge | sphere with brown fiber texture, drop shadow marker appears first |
| Hanging laundry line | slide under | thin rope, colored cloth planes |
| Incoming wave | lane dodge, timing | white foam wedge with scrolling wave texture and a warning flash |
| Crate stacks (market) | change lane or jump | cream and ink boxes with stripes |
| Low string lights | slide under | cable and small emissive spheres |

## 3. Collectibles and power-ups
- **Cashew (coin):** small kidney-shaped cashew built from a bent cone and a sphere, `--sun` tint, spins and bobs. Arc patterns along lanes.
- **$HHG token (rare):** cylinder coin with a canvas "H" face, `--hype-pink` rim, glow sprite. Fills the Hype meter.
- **Pav (health):** rounded box bun, restores the grace hit (max one stock). Rare.
- **Magnet, shield and boost visuals:** a coin vacuum ring, a translucent `--sun` bubble, and speed lines.

## 4. Characters (procedural)
- Body from capsule or cylinder parts: head sphere, torso, two arms and two legs as capsules, with simple run-cycle rotations (sin waves). Squash and stretch on jump and land.
- Outfit colors: Dev (pink hoodie, laptop bag), Designer (yellow jacket, beret), Marketer (cream shirt, megaphone).
- Slide: tilt the torso back and shorten the hitbox. Stumble: quick spin and recover.

## 5. The Demo Day clock (chaser)
Large torus ring in `--ink` with a `--cream` face, tick marks, a pink second hand that sweeps fast, and a canvas texture reading `DEMO DAY` and a countdown. It wobbles as it rolls and throws sparks when close.

## 6. Environment builders (recipes)
- **Palm tree:** 6 to 8 stacked tapered cylinders with a slight bend, 7 flat frond planes (bent along a curve) with white highlight stripes, a few coconuts. Outlined. Vary scale and tilt. Use instancing for far palms.
- **Beach shack:** box walls in cream, a thatch roof (cone or prism with a striped texture), two shutters (pink, yellow), a counter, a small signboard with a canvas-drawn word (for example "SUSEGAD CAFE", "FRESH FISH").
- **Portuguese house:** box with a terracotta pitched roof, window frames with shutters, a balcony with rails, a plaster color from the palette.
- **Church:** white main block, a triangular gable, two bell towers with domed tops, wide front steps, a cross.
- **Chapora fort wall:** crenellated boxes in a dark red-brown laterite tone with a slight color variation per block, cliff plane to the side.
- **Paddy strips:** long planes in `--leaf` with a slightly different tint per strip and a thin water channel with moving texture.
- **Water and waves:** plane with a canvas wave-line texture, scrolling UV, vertex sine motion if cheap.
- **Sky:** large inverted sphere with a vertical gradient shader or canvas texture per zone, a sun disc mesh, thin ray lines as a rotating plane texture.
- **Clouds and gulls:** flat white puffs from merged spheres, and white V-shaped line meshes flapping.
- **Fairy lights:** curved line with small emissive spheres, subtle flicker (night zone).
- **Neon sign:** canvas texture with glow, `--hype-pink` and `--sun`.
- **Road:** laterite red plane with painted `--sun` lane dashes, sand edges, props placed on both sides.

## 7. Canvas textures to generate
Wave lines, tile roof stripes, thatch stripes, awning stripes, net grid, fiber coconut, paper crowd confetti, neon letters, sun rays, film grain (for UI), clock face, sign lettering.

## 8. Chunk placement rules
- Chunk length 40 units. Each chunk gets: ground and edge scenery, 0 to 3 obstacle slots, 0 to 1 coin arcs, rare token or pav.
- Scenery lives 8 to 25 units off the lane center, never on the lanes.
- Always keep a safe path. Never place unavoidable walls across all 3 lanes without a jumpable or slideable option.
- Pool and reuse chunks. Remove far chunks, never allocate during a run.
