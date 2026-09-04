# Project K — "The Last Drop"
### Vertical slice build notes · cards S01-01 → S03-03

Built from `Kalki_The_Last_Drop_Interactive_Drama_Build_Spec.docx` v1.0. The spec's own build order says produce S01-01 through S03-03 first, then expand sequence by sequence — that's exactly what this is.

---

## ⚠️ Placeholder art, deliberately

The spec is explicit: *"Use placeholders where licensed likeness assets are unavailable. Never synthesize or approximate protected actor likenesses as final assets."* This build honours that literally.

- **No likenesses.** Every character is an abstract comic figure from the shared primitive. Nothing here approximates Prabhas, Amitabh Bachchan, or any approved model sheet.
- **No film-derived designs.** The vehicle is a greybox silhouette, not Bujji's approved transformation language. Characters are credited in-game as HUNTER, RIG, SCAVENGER, BROKER — not by film names — until likeness and naming rights are documented.
- **Ashwatthama's entrance** (last panel) is a scale silhouette only: feet-to-face vertical reveal, no face resolved.

Every one of these is a swap-in point, not a design decision. Replace with approved reference packs and the engine doesn't change.

---

## Spec compliance

| Spec requirement | Status |
|---|---|
| 9:16 portrait, safe-area aware, one-thumb | ✅ full-bleed, `env(safe-area-inset-*)` throughout |
| Authored cinematic camera, no joystick | ✅ panels + fixed-lane games only |
| Six input types: tap, timed tap, swipe, hold, rapid tap, drag | ✅ five built; **drag deferred** to S05-03 (drag-aim the machinery) |
| Soft fail, alternate outcome, immediate recovery | ✅ no fail state anywhere; a miss changes the caption |
| Resolve: 3-point, hidden outside clusters, refills between sequences | ✅ appears on first miss, resets on sequence change |
| Objective: one verb phrase at sequence start, then fades | ✅ TAKE THE JOB / REACH THE RUINS / CATCH THE CARRIER |
| Prompt colour: sand movement, teal context, red threat, **green only restoration** | ✅ green does not appear anywhere in this slice |
| Default reaction window 900 ms, perfect = central 30% | ✅ timing beats use a 16–20% gold zone, perfect at the inner 30% of it |
| Anticipation 300–700 ms before swipe prompts | ✅ chain cues open with the ring full, close over 1250 ms |
| Three misses in a cluster → assisted completion | ⚠️ **not built.** Runner and chain currently just accumulate misses. |
| State invariants (archive owner/condition tracked) | ⚠️ **not built.** No global state object yet — the slice ends before the archive matters (S06-02). |

---

## The eight cards

| ID | Card | Interaction built | Spec verb |
|---|---|---|---|
| S01-01 | Kashi marketplace | none — establishing | none |
| S01-02 | Inspect the job | **Spot-it**, 3 real among 4 decoys, 20 s | tap |
| S01-03 | Accept | **Hold** 1.2 s | hold |
| S02-01 | Wasteland run | **Lane runner** 32 s — swipe lanes, swipe up to clear pits, tap raiders | swipe + tap |
| S02-02 | Mark the carrier | **Timing tap** on a sweeping marker | timed tap |
| S03-01 | Rooftop chase | **QTE chain** — 7 cues: vault, slide, dodge, shoot, jump, dodge, catch | swipe + tap |
| S03-02 | Walkway collapse | **Rapid tap** sprint (22 taps) → **charge and release** leap | rapid tap + hold |
| S03-03 | Corner the scavenger | **Timing tap** grab | timed tap |

Dialogue is taken verbatim from §8 of the spec where the slice reaches it.

---

## What the anthology change means

The app is now `prototype/app.html` — a **library** with a shared engine. A story is pure data:

```
{ id, title, badge, blurb, theme{ink,paper,accent,cold,red},
  hud:{type:'clock'|'resolve', ...}, key, openCard,
  pages:[...],           // comic pages, panels, balloons, captions, SFX
  ix:{...},              // interaction definitions by kind
  order, map, outro }
```

Eight mini-game kinds are shared across stories — `runner, search, timing, hold, swipe, chain, mash` — each configured per story rather than duplicated. Seven Rains runs a 12-minute episode clock; The Last Drop runs Resolve. Same engine, different HUD, because the HUD is data.

Adding a third story is a data object and a set of scene builders. No engine work.

---

## Next, in spec order

1. **S04-01** — three deflections that converge (choice cards, no false branching)
2. **S05-01→04** — target taps, staff dodges, **drag-aim** the machinery, rapid-tap struggle → Rig ability
3. **S06-01→03** — the reveal. This is where green enters the palette for the first time, and where the global archive state object becomes load-bearing.

Before S06, build the state layer: `archive_owner`, `archive_condition`, `resolve`, `bounty_status`, `rig_condition` — and the continuity validator against §10's invariants.

---

## Art pipeline (v0.5)

The first pass was flat vector shapes. This one is a real rendering stack, still 100% inline SVG with no image assets — the whole app is one HTML file.

**Lighting model.** Hard warm key from the sun, cool sky bounce on the shadow side. That single rule does most of the work: every form has a lit plane, a core shadow, and an unbroken rim along the lit edge. Spec §4 asks for *"faces readable through motivated bounce light"* — this is how.

**The stack, back to front.**

| Pass | What it does |
|---|---|
| Sky | 3-stop vertical gradient, thin blue at altitude down to bleached haze at the horizon |
| Sun | Core disc plus a 3.2× radial bloom, blurred |
| Depth layers | Three ridge/dune bands, each hazed further toward sky colour — atmospheric perspective |
| Structures | Slab kit with a lit top edge, an occluded right edge, and damage cracks |
| Volumetrics | God-ray cones on `mix-blend-mode: screen`, blurred |
| Characters | Silhouette → skin gradient → core shadow → cheek hollow → brow ridge → features → gear → rim |
| Air | Deterministic dust motes (seeded PRNG, so panels are stable across reloads) |
| Grade | Radial vignette + `feTurbulence` grain on overlay |

**Faces.** Rebuilt around hard forms — heavy brow ridge, hooded eyes reduced to a sliver under a weighted lid, sunken cheek, cut jaw, dry downturned mouth. The rim light rides the *true* outer silhouette (hair included) rather than floating over it, which was the tell that made the first pass look like clip art.

**The entrance beat** (last panel of S03-03) uses a separate `kColossus` figure: small head against a massive body, wide stance, flared coat, and one unbroken lit edge running skull → shoulder → coat → boot. Scale reads from proportion and edge alone — no face is resolved, which is also what the spec wants for a reveal.

**Per-story treatment.** Seven Rains keeps the halftone comic look. The Last Drop switches to `data-art="film"`: thin ink, fine grain instead of halftone, translucent caption plates. Same engine, two different visual registers.

**Still placeholder.** Every figure is an original design and none of it is a likeness. The art quality is now high enough to read as intent rather than as unfinished, which makes it *more* important to say: these are not approved assets and the vehicle is not a film design. Swap points are unchanged.
