# THE BACKROOMS

A collection of first-person 3D exploration levels built entirely in vanilla HTML and JavaScript — no frameworks, no WebGL. Each level runs as a single self-contained `.html` file using a software renderer with perspective projection and the painter's algorithm.

---

## Controls

| Key | Action |
|-----|--------|
| `WASD` / Arrow Keys | Move |
| Mouse | Look |
| `Shift` | Run |
| `Space` | Jump (double jump supported) |
| `C` / `Ctrl` | Crouch |
| `Scroll Wheel` | Zoom |
| `E` | Destroy wall in front (Level 0 only) |

Mobile: left 45% of screen = joystick, right 45% = look camera.

---

## Levels

### Level 0 — The Floors (`level_0_-_The_Hub.html`)

**Tags:** `VERTICAL` · `SHAFTS` · `MULTI-FLOOR`

A procedurally generated multi-floor complex built from mathematical first principles. The world is an infinite grid of rooms stacked vertically, separated by concrete slabs of varying height (anywhere from a cramped crawlspace to a cathedral-scale void). Large vertical shaft systems carve through multiple floors at once, creating open drops and atrium-like spaces. Some floor cells are missing entirely, and others are pit rooms with walkable strip edges over real drops.

Falling too far into the abyss triggers a death screen. You can also stand on top of walls and double-jump between floors through holes and shaft openings. Press `E` to destroy the wall in front of you.

The renderer handles multiple floors simultaneously and uses a deterministic seeded RNG so the world is consistent between sessions.

---

### Level 1 — The Rooms (`level_1_-_The_Rooms.html`)

**Tags:** `INFINITE` · `CORRIDORS` · `PROCEDURAL`

An infinite grid of large rooms (2800×2800 units each) connected by hallways in all four cardinal directions. Every doorway leads somewhere — there is no way back, only forward into more rooms.

Each room is procedurally furnished with pillars and wall segments seeded from the room's grid coordinates. The starting room is empty; all others contain 2–5 randomly placed obstacles. Rooms use a blue carpet checkerboard floor, yellow walls with baseboards and crown moulding, and a warm concrete ceiling with a glowing light strip.

The renderer streams in rooms and halls as the player moves, preloading a 3×3 neighbourhood around the current room.

---

### Level 2 — The Corridor (`level_2_-_The_Corridor.html`)

**Tags:** `INFINITE` · `LINEAR` · `FORWARD`

One hallway. It runs forward and backward forever. There are no exits, no turns, and no other rooms. The corridor is 480 units wide and 320 units tall, rendered in infinite tiled segments along the Z axis. The floor alternates between two shades of blue carpet; the ceiling is warm concrete with a narrow glow strip.

The ambient audio includes a low resonant drone and fluorescent hum that give the space a long-tube acoustic character.

---

### Level 3 — The Passage (`level_3_-_The_Passage.html`)

**Tags:** `INFINITE` · `LATERAL` · `SIDEWAYS`

The same hallway as Level 2, but rotated 90 degrees. It runs left and right forever. The player starts facing the wall and must orient themselves laterally. Identical dimensions and palette to Level 2, but the corridor runs along the X axis instead of Z.

The drone is tuned slightly higher than Level 2, giving the lateral space a subtly different acoustic feel.

---

### Level 4 — The Intersections (`level_4_-_The_Intersections.html`)

**Tags:** `INFINITE` · `CROSSING` · `JUNCTION`

Two hallways cross at a single point at the origin. One runs forward/backward (Z axis), one runs left/right (X axis). Each arm extends infinitely in both directions. The junction square where they meet is open on all four sides, with small corner pillar highlights marking each inner edge.

Wall panels on each arm are interrupted at the junction so the corridors genuinely open into each other. The collision system allows free movement within the cross shape while blocking entry into the solid corner quadrants.

The ambient audio uses three oscillators and a longer reverb to suggest the acoustic complexity of a junction point.

---

### Level 5 — The Pool (`level_5_-_The_Pool.html`)

**Tags:** `AQUATIC` · `VERTICAL` · `INFINITE`

A single enclosed room (1800×2400 units) with blue carpet, yellow walls, and a warm ceiling. At its centre sits a pool (800×1400 units) whose water surface sits flush with the floor. The pool has no bottom — the inner walls descend 8000 units before a floor tile appears, giving a credible illusion of infinite depth.

Walking over the pool edge causes the player to fall in. In the water, buoyancy pushes the player upward naturally; holding `C`/`Ctrl` dives them down. The camera transitions to an underwater tint and vignette overlay when fully submerged. Swimming replaces footstep sounds with splash audio. The water surface is animated with a shimmer overlay drawn as screen-space sine wave lines.

---

### Level 6 — The Outside (`level_6_-_The_Outside.html`)

**Tags:** `INFINITE` · `OPEN` · `OUTSIDE?`

No walls. No ceiling. An infinite tiled plane of blue carpet under a solid yellow sky. The sky is the wrong shade of yellow — familiar but not quite right. Fog blends the floor into the horizon colour, creating a glowing haze band. There are no obstacles and no boundaries.

The audio is intentionally sparse: faint wind noise and a barely audible distant hum, with almost no reverb. The absence of enclosed space is the point.

---

## Technical Notes

All levels share the same core renderer:

- **Software 3D** — perspective projection with a painter's algorithm polygon queue (depth-sorted by centroid distance).
- **Near-plane clipping** — polygons are clipped against the near plane before projection.
- **Fog** — linear fog blends geometry toward a background colour starting at a configurable distance.
- **Audio** — Web Audio API procedural synthesis. Each level generates footstep sounds, a landing thud, convolution reverb (built from noise impulse responses), and an ambient drone. No external audio files.
- **Mobile support** — split-screen touch controls (joystick left, look right), pointer lock on desktop.
- **PWA** — Level 0 includes an inline service worker and manifest for offline/installable support.

---

## File Structure

```
index.html                        ← Level select menu
level_0_-_The_Hub.html            ← The Floors (multi-floor procedural)
level_1_-_The_Rooms.html          ← The Rooms (infinite procedural grid)
level_2_-_The_Corridor.html       ← The Hallways (forward/backward)
level_3_-_The_Passage.html        ← The Hallways (left/right)
level_4_-_The_Intersections.html  ← The Intersections (crossing corridors)
level_5_-_The_Pool.html           ← The Pool (swimming, infinite depth)
level_6_-_The_Outside.html        ← The Outside (open sky, no walls)
```

Open `index.html` in any modern browser to start.
