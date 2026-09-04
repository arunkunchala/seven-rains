# Episode Pacing — Comic Panels × Hypercasual Mini-Games
### v0.3 structure · one 12-minute episode

**The model:** the story is told in comic-book pages (tap to reveal the next panel or balloon, like a guided-view comic reader). Roughly every 60–90 seconds the page hands off to a **hypercasual mini-game** (20–40s, Subway-Surfers / Fruit-Ninja / spot-it style) or a **single QTE** (2–5s, one gesture) that is the story's action beat. Then back to pages. The mini-game *is* the scene — you don't watch Vidya ride through the flood, you ride it.

**Why this shape:** microdrama craft says a hook every 90 seconds and a payoff inside each one. Hypercasual says a 20–40s loop with instant readability. Those two cadences nest cleanly — one mini-game per micro-episode. And comic panels are the cheapest possible way to convey a story with clarity: a face, a balloon, a caption. No ambiguity about who is speaking or what just happened.

---

## Density rule

| | Per episode (12 min) | Per sequence (~3 min) |
|---|---|---|
| Comic pages | 36–44 | 9–11 |
| Panels | 70–90 | 18–22 |
| **Mini-games** (20–40s, dozens of inputs) | **7–8** | 2 |
| **Single QTEs** (one gesture, 2–5s) | **10–14** | 3 |
| Interaction *moments* | ~20 | 5 |
| Raw input events | 300+ | — |

Twenty moments across twelve minutes is one every ~36 seconds on average — but they cluster. A sequence reads as: **pages → small QTE → pages → BIG mini-game → pages → small QTE → pages → hook.** Never two mini-games back to back. Never more than ~90 seconds of pages without a hand on the screen.

Reading time per page is player-controlled (tap to advance); the 12:00 episode clock runs regardless, so a slow reader spends their slack in the pages, not the games.

---

## Episode 1 — "First Rain" — pacing map

| Time | Seq | Pages | Interaction moments |
|---|---|---|---|
| **0:00–3:30** | **1 · The Call** | Cold open (tower, body, phone) · Farhan's call · the ride · Rathore at the tape · the scene · "seven days" · the boy on the curb | **QTE** swipe to answer · **MINI** lane runner (ride through the flood, 30s) · **QTE** timing tap (duck under the tape) · **MINI** spot-the-clue (3 details, 22s) · **QTE** hold your ground |
| **3:30–6:15** | **2 · The Guard** | Security office · Salim's statement · the badge log · Farhan finds the gap · press outside | **MINI** tell-tap interrogation (rhythm, 30s) · **QTE** drag the log scrubber to 03:41 · **MINI** swipe-slash the press mics (Fruit Ninja, 20s) · **QTE** slam the door |
| **6:15–9:00** | **3 · The Fourth Floor** | Stairwell climb · Anaya's desk · the team · Tanvi helps · Kiran's alibi · the photo | **MINI** stair-climb rhythm tap (25s) · **MINI** desk search spot-it (22s) · **QTE** pinch/hold to focus the pod photo · **QTE** say nothing (hold, 4s) |
| **9:00–12:00** | **4 · The Boy** | Driving to the station · Farhan: nobody came for him · kneel · the drawing · **the raincoat** | **MINI** lane driving through traffic (30s) · **QTE** kneel (slow drag) · **QTE** unfold · **QTE** look closer · **QTE** hold — the last look |

**Hooks at each sequence end:** 1 → the boy has been holding a folded paper since six. 2 → the loading bay isn't on the badge system. 3 → Tanvi's desk hook is empty. 4 → *"She gave me a chocolate."* — the woman in the yellow raincoat, across the street, waving at the boy.

The best reveal of the day sits at 11:40, not 3:00.

---

## Mini-game library (hypercasual reference → story use)

| Reference | Verb | Story use in Case One |
|---|---|---|
| Subway Surfers | 3-lane runner, swipe to dodge/jump | Ride through the flood (E1) · foot chase through Shivajinagar (E4) |
| Traffic Racer | lane driving, tap-hold brake | Drive to the station (E1) · airport road intercept (E7) |
| Fruit Ninja | swipe-slash targets | Press mics (E1) · tearing evidence tape (E3) |
| Spot-it / Hidden object | tap the real ones among decoys, timer | Crime scene (E1) · Anaya's desk (E1) · the evidence locker (E6) |
| Rhythm / Piano Tiles | tap on the beat | Stair climb (E1) · interrogation tells (E1, E4, E7) |
| Timing tap / Stack | tap when the marker is in the zone | Duck under tape (E1) · badge the door before it locks (E3) |
| Flappy / Hold | hold within a band | Steady the camera (E3) · hold your ground (E1) |
| Scrubber | drag a timeline to a moment | Badge log (E1) · CCTV re-sync (E5) |
| Draw-a-line | connect points in order | Phone tower pings (E5) · the case board (E7) |

Every mini-game has three outcomes (CLEAN / ROUGH / MISSED) and no fail state — the story continues, the caption on the next page changes. Twelve games, each one a data row with tunable difficulty, reskinned per episode. Same library rule as before: no game twice in a sequence, and a repeat within an episode carries a modifier.

---

## Visual language

Two-tone noir comic with one accent. Ink black, paper cream, amber for light/the raincoat, cold blue for rain and night, red only for SFX and danger. Thick panel borders, halftone shading, heavy shadow on one side of every face. Balloons in uppercase condensed. SFX lettering only where a sound matters (BRRRR, SWISH, SPLASH). Captions in black bars carry time, place and Vidya's inner voice.

In production the panels are illustrated frames — far cheaper than live action, fully controllable, and the frame-by-frame cut between panel and mini-game is seamless because both are drawn in the same ink.
