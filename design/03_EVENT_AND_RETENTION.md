# SEVEN RAINS — Live Event & Retention Layer
### Design spec v0.1

This is the layer that turns a 7-part story into a 7-day *event*. It is where most microdrama-in-game experiments fail, so it gets its own document.

---

## 1. The daily loop

```
19:59  Pre-notification ("The case reopens in 1 minute")
20:00  LIVE. Notification ring. Event tile pulses in the game's hub.
20:00–21:30   START WINDOW (90 min). Player may begin any time in here.
[on start]    12:00 hard timer begins. Episode runs to completion.
[on finish]   Case Board. Cliffhanger. "Day N of 7. Come back tomorrow, 20:00."
21:30  Window closes. Non-starters are marked missed for the day.
```

### Why a 90-minute start window and not a 12-minute one
A 12-minute hard window means one dinner, one commute, one crying child = a broken streak on Day 3, and a player who now has no reason to come back on Days 4–7. The 90-minute start window preserves the *feeling* of appointment television (everyone plays the same evening, the community discusses the same episode) while surviving contact with real life.

The **12 minutes remains hard** once started. That's where the tension lives, and it's honest: you can choose when to sit down, but once you do, you're in it.

---

## 2. Missing a day

Missing days is the single largest churn risk. The design assumption should be that **a meaningful share of players will miss at least one of the seven days**, and the system must make Day 7 still worth showing up for.

| State | Player experience |
|---|---|
| **Missed 1 day** | Next login offers **Case File Replay** — the missed episode, playable, no timer, at **60% clue yield**. Takes ~8 min. Available for 24h only. |
| **Missed 2 days** | Both replays offered; the second at 40% yield. Vee's voiceover acknowledges the gap ("I lost a day. It happens."). |
| **Missed 3+ days** | Replays still offered, but the player is told plainly they're unlikely to reach the top ending this run — and offered a **Rerun** slot when the case cycles back. Honesty beats false hope here; players who feel misled about their chances churn harder than players who are told they're behind. |

**Rerun cycling:** the case re-runs on a rotation (e.g. every 3–4 weeks) with the *same* story. Players who missed it get a clean shot; players who completed it get a **Cold Case** variant — same episodes, tighter windows, one clue relocated, and a hidden eighth ending. Reruns are how you amortise the enormous per-case content cost across a live-ops calendar.

---

## 3. The Case Board (meta-progression)

The Board is the game's memory and its "come back tomorrow" surface. It persists between episodes and is browsable any time from the hub — including outside the event window, which matters: it gives players a reason to open the game at 11am.

**Structure:**
- **Evidence cards** (physical clues) — earned Clean/Rough/Missed as described in the interaction spec.
- **People cards** (the six suspects) — each has an alibi slot, a motive slot, and a lie slot. Slots fill as clues are earned.
- **Threads** — the player can manually draw connections between cards. This is *not* scored during Days 1–6. It is pure expressive play; it exists so the player builds a mental model.
- On **Day 7 Act 3**, the threads they've already drawn are pre-loaded into the accusation sequence. A player who has been theorising all week gets a real mechanical head start. A player who hasn't is doing it cold under a timer.

That asymmetry is the whole retention argument for the Board: **thinking about the case between episodes is mechanically rewarded, without requiring it.**

**Card ledger for Case One:** 20 evidence cards total across Days 1–6, plus 2 epilogue-gated cards per episode (12 more) = 32 obtainable. Day 7 endings gate at 8 / 13 / 18 (see Story Bible §9). A perfect run yields 32; the top ending needs 18 *plus* a 7/7 streak. That means a strong player who missed one day can still reach the third-best ending — which is the correct generosity setting.

---

## 4. Streaks and rewards

Keep the reward structure inside the fiction wherever possible; a microdrama that showers you in currency stops being a drama.

| Day | Completion reward |
|---|---|
| 1 | Case Board unlock; cosmetic: *Crime Branch* profile frame |
| 2 | Small hard-currency drip |
| 3 | Cosmetic: Vee's coat (wearable in the parent game if the fiction allows) |
| 4 | Small hard-currency drip |
| 5 | **Streak checkpoint** — a bonus clue card, free, for 5/5 |
| 6 | Cosmetic: the yellow Kalpa rain jacket (this is a *spoiler-shaped* reward and lands beautifully on rewatch) |
| 7 | Ending-scaled: title, frame, and the **"Seven Rains" ending unlock at 7/7** |

**No paid continues. No paid clue hints. No energy gate.** The moment a player can buy their way to the ending, the deduction is worthless and the format's core promise dies. Monetise this on cosmetics, the parent game's economy, and the attention it drives — not on the mystery.

---

## 5. Notification design

Seven notifications in seven days is a lot of permission to spend. Each one must earn it.

- **Never generic.** Not "Your event is live!" — instead a line from the fiction that is also a hook:
  - Day 2: *"The badge log has one name on it. It's the wrong one."*
  - Day 4: *"Salim finally told me where he was. It's worse."*
  - Day 6: *"The paint came back. She didn't fall."*
  - Day 7: *"She has a flight at nine. The warrant is at nine."*
- **One per day, at a user-chosen hour.** Let the player pick their slot at event opt-in (20:00 default, options at 13:00 / 18:00 / 20:00 / 22:00). A player who chose their time does not experience the notification as an interruption.
- **Silent after the first miss.** If a player skips two days, drop to one summary notification and stop. Recovering a lapsed player is worth less than not annoying a returning one.

---

## 6. Social layer (low cost, high leverage)

Microdramas thrive on same-day discussion. Cheapest useful version:

- **Daily verdict poll.** After each episode: *"Who do you think did it?"* — results shown as a live percentage bar. On Day 3 the entire playerbase will pick Kiran Menon. On Day 7, showing them that bar again is the single best moment in the event.
- **Spoiler-safe by construction.** Poll results are gated to players at the same day-index. Someone on Day 2 never sees Day 5 data.
- **Shareable Case Board snapshot.** One-tap export of the player's board with their threads drawn. Free marketing, and it's the artefact that makes non-players ask what it is.

---

## 7. Instrumentation — what the POC must measure

Ranked by what would actually change the design:

1. **Per-beat tier distribution.** Any beat where MISSED exceeds ~25% is mistuned; any beat where CLEAN exceeds ~90% is free and should be tightened or cut.
2. **Drop-off timestamp within the 12 minutes.** Cluster analysis. A spike at a specific beat is a broken beat, not a bored player.
3. **D3_HOLD first-encounter success rate.** The headline design bet. See interaction spec §10.
4. **Day-over-day return rate**, split by ending-tier trajectory. Do players who are behind on cards return less? If yes, the catch-up generosity is too tight.
5. **Start-time histogram within the 90-min window.** Tells you whether the window should be wider, narrower, or moved.
6. **Board opens outside the event window.** The single best proxy for whether the case has actually got its hooks in.

---

## 8. Production reality check

Rough per-case content load, so the POC scope decision is made with eyes open:

- 7 episodes × ~34 beats = **~240 authored interactions** per case
- ~85 minutes of runtime, of which perhaps 20 minutes is unique cinematic content and the rest is interaction-driven scene work
- 6 speaking characters, ~2,500 lines of VO

The way this becomes viable is **the beat library**. Twenty verbs, each with a tunable data row and a reskinnable presentation layer, means the 240 interactions are 240 *rows*, not 240 bespoke builds. Getting the verb library and the build-time linter right is worth more than getting Episode 1 right, because it's what makes Cases Two through Ten affordable.

**Recommended POC cut:** build **Episode 1 complete** plus the **Day 7 Act 3 accusation** — the opening that proves the moment-to-moment feel, and the finale that proves the payoff is worth seven days. Skip Episodes 2–6 entirely for the first internal test. If those two ends work, the middle is a content problem, not a design risk.
