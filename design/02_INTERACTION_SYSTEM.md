# SEVEN RAINS — Micro-Interaction System
### Design spec v0.1

---

## 1. First principles

Five rules that everything else obeys.

**R1 — The story never stops.** There is no retry, no game-over, no "try again" screen. Every interaction resolves in one attempt and the scene continues. What changes is *what Vee walks away knowing.* This is non-negotiable for a 12-minute daily event: a player who gets stuck at minute 4 is a player who churns.

**R2 — Three tiers, never two.** Every interaction resolves as **CLEAN / ROUGH / MISSED**. Clean is a tight window, Rough is a generous one, Missed still advances. Binary pass/fail makes a 40-interaction episode feel like an exam. Three tiers make it feel like performance.

**R3 — No tutorials, ever.** Every interaction must be readable in **under 300ms** from a glyph plus the object's own physics. A dial that jitters wants turning. A drawer with a crack of light wants prying. If a designer needs a text prompt to explain a beat, the beat is wrong.

**R4 — One body.** Every gesture is something Vee's hands or feet are doing. No abstract puzzles, no sliding-tile locks, no "hack the computer" minigames. The player is operating a person, not a UI.

**R5 — A verb never repeats identically.** See §6.

---

## 2. The time model

| Quantity | Value |
|---|---|
| Real-to-drama ratio | **1 real second = 2 drama minutes** (30s = 1hr) |
| Episode real length | **720s (12:00)** |
| Episode drama span | 24 drama-hours — one full day, with hard cuts compressing sleep and dead travel |
| Interactions per episode | **28–44** (target 34) |
| Mean beat length | **~18s** (≈36 drama-minutes) |
| Longest gap with no input | **11s** — hard cap. Past that the player's attention leaves the screen. |

### The Case Clock
A persistent HUD readout showing in-fiction time, ticking at 2 drama-minutes per second. It is not decoration — it is the **penalty surface**:

- **CLEAN** → no cost, sometimes a small time refund (−5 drama-min)
- **ROUGH** → +5 drama-min
- **MISSED** → +15 drama-min

Time debt does **not** shorten the player's 12 minutes. It advances the in-fiction clock, and the in-fiction clock gates the **Epilogue**: each episode has an optional final scene that only opens if the Case Clock is under a threshold at the resolution beat. The epilogue is worth 1–2 clue cards.

So: *sloppy play costs you knowledge, never playtime.* This preserves the fixed 12-minute event window while making skill genuinely matter.

---

## 3. The gesture vocabulary — 20 verbs, 5 classes

Each verb is listed with its input, its "tell" (how the player knows without being told), and its tuning knobs.

### Class A — TRAVERSAL (≈30% of beats)
Fast, rhythmic, low-cognition. These are the connective tissue and the place dialogue gets delivered.

| # | Verb | Input | Tell | Tuning |
|---|---|---|---|---|
| A1 | **Sprint** | Alternating taps, L/R zones, on the footfall beat | Footstep ghosts pulse ahead of the foot | BPM, tolerance ±ms |
| A2 | **Vault** | Single upward swipe at the approach threshold | Obstacle edge flares white as it enters range | window ms |
| A3 | **Weave** | Continuous horizontal drag to steer through a crowd/traffic | Gaps glow; bodies drift laterally | gap width, closure speed |
| A4 | **Drive** | Two-thumb: drag to steer, tap-hold right pad to brake | Lane markers, brake-cue chevrons | traffic density |
| A5 | **Descend** | Rapid repeated down-swipes, tempo-matched | Stair rail blurs at correct tempo | required tempo |
| A6 | **Squeeze** | Pinch-in and hold to slip through a gap | Gap edges pulse inward | hold duration |

### Class B — MANIPULATION (≈25%)
Slow, tactile, resistance-based. The satisfying ones. These carry the "physical presence" of the show.

| # | Verb | Input | Tell | Tuning |
|---|---|---|---|---|
| B1 | **Turn** | Rotary drag around a pivot — keys, dials, valves, doorknobs | Object jitters against its stop | total arc, sticking point, torque curve |
| B2 | **Pry** | Press and drag against simulated resistance | Crack of light along the seam | resistance, break threshold |
| B3 | **Peel** | Slow drag inside a *tolerance band* — too fast and it tears | Material stretches and whitens near tearing | band width, length |
| B4 | **Steady** | Hold pointer inside a drifting reticle for N cumulative seconds | Reticle wobble amplitude | drift speed, radius, duration |
| B5 | **Align** | Drag two elements into register | Ghost outline of the target position | snap tolerance, rotation axis |
| B6 | **Thread** | Trace a narrow path without leaving it — a wire, a lockpick, a suture | Path walls flash on contact | corridor width, length |

**B3 (Peel) is the signature verb of the series.** Nothing else in mobile games feels like being told *go slowly, but not too slowly.* Use it for the highest-stakes evidence moments — lifting a print, separating rain-fused paper, pulling a photo from an album.

### Class C — INVESTIGATION (≈25%)
Perception under time pressure. Where the actual detective work lives.

| # | Verb | Input | Tell | Tuning |
|---|---|---|---|---|
| C1 | **Sweep** | Drag a torch/UV cone across a dark surface, hold on the anomaly | Anomaly returns a faint shimmer at cone edge | cone width, anomaly size, hold ms |
| C2 | **Magnify** | Pinch-zoom into a photo until a detail resolves, then tap it | Detail blooms into focus past a zoom threshold | zoom depth, decoys |
| C3 | **Sift** | Repeated swipes to clear layers — dust, papers, silt, rubble | Layer edge lifts under the finger | layer count, tempo |
| C4 | **Contrast** | Tap the one element that changed between two frames | Both frames shown; no highlight | delta subtlety, timer |
| C5 | **Trace** | Draw a path connecting points — spatter trajectory, tower pings, a route on a map | Points pulse in sequence order | point count, ordering constraint |
| C6 | **Listen** | Hold to isolate a channel, scrub a waveform to find a buried sound | Waveform swells at the target | clip length, needle width |

### Class D — PRESSURE (≈15%)
Interrogation and confrontation. The only class where the *target* is a person.

| # | Verb | Input | Tell | Tuning |
|---|---|---|---|---|
| D1 | **Interrupt** | Tap during the ~400ms window a suspect's tell appears | A microexpression: a swallow, a glance down, a hand to the collar | window ms, tell subtlety |
| D2 | **Choose** | Pick one of 2–3 lines before a collapsing timer bar | Bar drains; lines fade in order | duration, option count |
| D3 | **HOLD** | **Do nothing.** Any input fails the beat. | Everything invites a tap; nothing should be tapped | silence duration |
| D4 | **Press** | Repeated taps raise a pressure meter — but overshoot and the suspect lawyers up | Two-zone meter with a moving safe band | band width, drift |

**D3 (HOLD) is the most important verb in the game.** It is the only one that punishes the reflex the other nineteen train. Introduce it in Episode 3, reprise it in 5, and make it the winning move of the Day 7 confrontation. A player who has learned to sit still through six seconds of silence has learned something the game never told them.

### Class E — SET PIECE (≈5% — one or two beats per episode, always the climax)
Modifiers stacked on existing verbs rather than new verbs. Used sparingly; they burn out fast.

| # | Modifier | Effect |
|---|---|---|
| E1 | **Two-hand** | Two simultaneous holds while a third element needs a tap |
| E2 | **Invert** | Controls mirror — concussion, smoke, panic |
| E3 | **Blind** | Screen darkens; the beat resolves on audio cues only |
| E4 | **Stack** | Two Class A/B verbs run concurrently in split zones |

---

## 4. Anatomy of a beat

Every beat in the build is one data row:

```
BEAT {
  id            "E1_B14"
  verb          C1_SWEEP
  modifier      none
  duration_ms   9000            // hard window
  clean_ms      3200            // clean threshold
  tolerance     0.65            // verb-specific accuracy scalar
  tell_ms       260             // how long the affordance shows before input opens
  yields        { clean: "C2_PAINT_FLECK_FULL",
                  rough: "C2_PAINT_FLECK_PARTIAL",
                  missed: null }
  clock_cost    { clean: -5, rough: +5, missed: +15 }
  vo            "FARHAN_E1_14"  // plays across the beat, never blocks it
}
```

Two rules that fall out of this shape:

- **Dialogue never blocks input.** VO runs over beats. There is no "listen to this line, then act." In 12 minutes you cannot afford a single second of hands-idle exposition.
- **Every beat has a `missed` path that still writes state.** Even a miss produces a scene transition; it just writes `null` to the clue slot.

---

## 5. Difficulty curve

| Ep | New verbs | Retired | Beats | Clean window | Notes |
|---|---|---|---|---|---|
| 1 | A1, A2, B1, B4, C1, C2 | — | 28 | 1.00× | Widest windows. Teach by doing. |
| 2 | B2, C3 | A2 | 31 | 0.95× | First Peel tease |
| 3 | B3, D1 | — | 33 | 0.90× | **D3 HOLD introduced, unsignposted** |
| 4 | C4, D2 | B1 | 35 | 0.85× | First E-class modifier (Invert) |
| 5 | A3, C5 | C1 | 37 | 0.80× | Density peak of Act 2 |
| 6 | B5, C6 | A5 | 39 | 0.78× | Two set pieces |
| 7 | A4, B6 | — | 44 | 0.75× | All classes; D3 is the climax |

Windows scale from a per-verb base. The curve is intentionally shallow — **the difficulty ramp is density and novelty, not reaction time.** Reaction-time ramps exclude older and casual players, who are a large share of an in-game event audience.

---

## 6. The anti-repetition rules

The user requirement was "simple yet challenging, intuitive and non-repetitive." Repetition is the failure mode most likely to kill this format, so it gets hard constraints the content tools should *enforce at build time*, not leave to authorial discipline:

- **The 90-second rule.** No verb may appear twice within 90 seconds of real time.
- **The reprise rule.** A verb's second appearance *in an episode* must carry a modifier: a distractor, a moving target, an inverted axis, a shortened window, or a stacked second verb. Never the same beat twice.
- **The 2-in-1-out rule.** Each episode introduces exactly two new verbs and retires one. Novelty every day; total vocabulary never exceeds what a thumb can hold.
- **The class-run cap.** No more than three consecutive beats from the same class. Traversal → Traversal → Traversal → *must* break to another class.
- **Context reskin.** A verb should never appear in the same fictional object twice in a case. B1_TURN is a car key in Ep1, a stairwell fire-valve in Ep3, a rotary evidence-locker dial in Ep6. Same input, three different feels.

A build-time linter that fails the episode on any of these violations is genuinely worth the two days it takes to write.

---

## 7. The 12-minute episode template

| Window | Act | Beats | Class mix | Function |
|---|---|---|---|---|
| 0:00–0:45 | **Cold open** | 2–3 | A, D2 | Recap sting; warm the thumbs; re-establish stakes |
| 0:45–3:00 | **Approach** | 6–8 | A-heavy | Get Vee to the scene. Farhan delivers exposition over it. |
| 3:00–6:30 | **The Scene** | 9–12 | B + C | The slow tactile core. Where the clues actually are. |
| 6:30–9:30 | **The Person** | 5–7 | D-heavy | One confrontation. The episode's emotional beat. |
| 9:30–11:15 | **Escalation** | 6–10 | E set piece | Density spike. Highest beats-per-second of the episode. |
| 11:15–12:00 | **Board & Sting** | 2–3 | C5, tap | Pin the clue cards. Cliffhanger. Close. |

The rhythm is deliberately **fast → slow → talk → fast → stop.** A flat density curve for 12 minutes is exhausting; the Scene act at 3:00–6:30 is the breath that makes the 9:30 spike land.

---

## 8. Feedback and juice

Non-negotiable per beat, because at this cadence feel *is* the product:

- **Pre-input:** the tell (glyph + object physics) for 200–300ms.
- **On contact:** immediate visual response within one frame. No input latency budget above 50ms.
- **On resolve:** tier-coded — CLEAN is a white flash and a rising tick; ROUGH is amber and a flat tick; MISSED is a desaturation pulse and a low thud. Distinct enough to read peripherally without stopping.
- **Haptics:** light impact on contact, medium on Clean, double-tap on Missed. On Android, respect the system haptic setting.
- **Never a modal.** No "Clue Found!" popup. Clue acquisition is a card sliding into the corner while the scene keeps moving.

---

## 9. Accessibility (this format is unusually hostile without it)

- **Assist Mode:** all windows ×1.5, Clean thresholds ×1.4. Available from the pause menu, no penalty, no shame copy. Roughly 15% of an in-game event audience will need it.
- **Every audio-only beat (E3_BLIND, C6_LISTEN) needs a visual channel** — waveform, directional indicator.
- **Every colour-coded tier needs a shape** — CLEAN is a circle, ROUGH a triangle, MISSED an X.
- **One-handed reachability:** no required input above the top 25% of the screen, no simultaneous inputs more than 60% of screen width apart except in explicit E1 two-hand set pieces (which must have a one-handed fallback).

---

## 10. Open questions for the POC build

1. **Does B3_PEEL survive on a phone?** The tolerance-band drag is the riskiest verb in the set. Prototype it first; if it doesn't feel good in 20 minutes of tuning, cut it before it becomes load-bearing.
2. **Is 34 beats/12 min too dense on a small screen?** Instrument the POC and check for input-error clustering after minute 8 — that's the fatigue signal.
3. **Does D3_HOLD read at all without a tutorial?** Highest-risk design bet in the document. If under 30% of testers hold on the first encounter, it needs a *diegetic* teacher — Farhan saying "let her talk" once, in Episode 3, and never again.
4. **Portrait vs landscape.** Portrait is correct for the event context (one hand, notification-triggered) but costs the Class A traversal beats a lot of visual room. Test A3_WEAVE in portrait early.
