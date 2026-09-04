# Art pipeline — where the visuals actually come from

Written after a fair question: *why are we doing development art?*

## The honest constraint

Claude has no image generation in this session — no diffusion model, no Blender, no renderer. Everything shipped so far is drawn in code, because code is the only thing that can be emitted. That is a tooling limit, not an art direction. Treat every visual in `prototype/app.html` as **greybox**, however well-lit it has become.

## The three real paths

| Path | What it buys | What it costs | Verdict |
|---|---|---|---|
| **AI-generated 2D plates** | Shipping-quality art at 10–50× lower cost than traditional production (the figure from the China research). Matches the spec's own §12 guidance: generate environment plates without characters, composite approved character renders over them. | Character consistency is the hard part — 67% of practitioners name it as their number one obstacle. Needs reference sheets, seed discipline and a human art-direction pass. | **The main line.** This is how the episode should actually look. |
| **Real-time 3D** | Depth, one light rig across all 26 cards, the camera becomes a tool instead of a drawing. | Needs modelled, rigged, textured characters. Procedural 3D humans look worse than drawn ones, and this format lives on faces. Battery and thermals over a 12-minute daily session. | **Action beats only.** See below. |
| **Hand-coded vector** | Free, instant, zero assets, fully controllable. | Never reads as a shipping mobile game. | **Greybox only.** Its job is to hold the layout until real art lands. |

## The 3D test, and what it settled

`prototype/wasteland-3d.html` rebuilds card **S02-01** as real 3D — raw WebGL2, no library, no image assets. Scrolling noise-displaced terrain, a road corridor cut into it, a low warm sun with cool sky bounce, height fog that scatters toward the light, mesas and the Complex stack hazed by distance, bloom + ACES + grain.

**What 3D clearly wins:**
- Depth is free. Obstacles occlude and scale correctly without hand-authoring three parallax layers per scene.
- One light rig relights every shot. Move the sun, all 26 cards update. In 2D each panel is lit by hand.
- The camera becomes a tool. Push-ins, orbits and the spec's *"feet-to-face vertical reveal"* are camera moves, not new drawings.
- Frame-rate independence and procedural variety — the road never repeats.

**What 3D clearly loses:**
- **Faces.** There isn't a single close-up in that test, because procedural 3D humans look worse than drawn ones. The vertical frame exists for faces and hands; that is the format's whole engine.
- It needs an art team. The test looks decent because it is rocks, sand and boxes — the cheapest possible subject.
- Cost per minute of battery is far above panels.

**Conclusion: split by beat type, not by taste.**

| Beat type | Cards | Treatment |
|---|---|---|
| Traversal / action | S02-01, S03-01, S03-02, S07-03, S08-01, S09-01, S10-01 | **Real-time 3D.** Motion, depth and camera are the point. |
| Dialogue / reveal / intimacy | S01-01→03, S04-01, S05-04, S06-01→03, S11-01, S12-01 | **2D plates.** Faces, hands, performance. AI-generated and composited. |

The spec's own shot list splits almost exactly along that line, which is a good sign the division is real rather than convenient. It is also what most high-end mobile narrative games already ship.

## Two engineering notes from building the test

- **Never trust a frame-rate counter that averages clamped delta time.** The first version reported 24 FPS while actually running at 4 — the dt clamp made the simulation run in slow motion and the counter averaged the clamp, not reality. Measure with raw wall clock, clamp only what feeds physics.
- **Spawn on distance, not on time.** Time-based spawning piles obstacles up on slow devices and thins them out on fast ones. `scroll - lastSpawnZ > gap` is identical on every phone.

## What to do next

1. Build the **reference sheet + prompt pack** for the six characters and eight environments — that is the artefact the art lead needs, and consistency is won there.
2. Keep the greybox app as the **layout and timing reference**; art drops into slots without touching the engine.
3. Only invest in 3D for the seven traversal cards, and only once there are modelled hero assets.
