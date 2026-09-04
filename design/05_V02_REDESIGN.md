# What v0.1 Got Wrong, and v0.2
### Audit against the market research · September 2026

Read `04_MARKET_CONTEXT.md` first. This document is the honest post-mortem on v0.1 and the redesign that follows from it.

**The one-line verdict:** v0.1 is a well-built detective game with a microdrama schedule bolted on. It is not a microdrama. Almost every craft rule that the format actually runs on is either absent or inverted.

---

## 1. The biggest problem is the genre, and it was my choice, not yours

You asked for a detective theme and I took it without examining it. That was the mistake, because:

**A murder mystery is a deferred-gratification genre. Microdrama is a compressed-gratification genre. They are structurally opposed.**

The whole pleasure of a whodunit is *withholding* — the answer is worth having on Day 7 precisely because it was denied on Days 1 through 6. The whole pleasure of microdrama is **爽点 delivered inside 90 seconds**: the humiliation is staged publicly, the reversal is witnessed by the humiliators, and the payoff lands before the episode ends. Chinese writers' rooms treat sustained suffering (虐) without a counterbalancing reversal (爽) as a **named failure mode**.

v0.1 is 虐 for six days followed by one 爽. That's a season of prestige TV. It is the opposite of the format.

### Three ways out, in order of how much I'd bet on each

**Option A — Procedural chassis, revenge engine (recommended).**
Keep the case, keep Vidya, keep the 7-day clock. Change what the *episodes* are about. Every episode gets a personal antagonist beat with a payoff inside that episode: someone dismisses her, and inside the same 90 seconds she makes them eat it. The case is the plot; the drama is Vidya against the people who want her gone. Concretely: **DCP Rathore, who signs Salim's warrant, is the man who ended her career in Chennai.** Now she has a face to beat, weekly, in public.
*Cost: a rewrite of the episode structure, not the case. The bible survives.*

**Option B — Swap to the proven canon.** Rebirth-revenge, contract marriage, status reversal, secret identity. Highest expected performance, biggest rewrite, and least differentiated — this is what 192,000 titles a year already are.

**Option C — Keep v0.1 as designed** and accept we're making a prestige serial with microdrama scheduling. Defensible if the parent game's audience skews toward players who want depth, but it forfeits the format's proven engine.

I'd build A. It keeps the work we've done, it's differentiated (nobody is making detective microdrama well), and it imports the emotional cadence that actually retains.

---

## 2. The seven specific failures

**1. No human being in the first ten seconds.** The prototype opens on a ringing phone. The rule is: 0–3s golden hook, and by 0:10 the viewer must have the core conflict, the character relationships and the protagonist's objective. **~30% of viewers churn inside 3 seconds if not hooked.** We opened on furniture.

**2. Twelve minutes is one session, not one episode.** Real microdramas run 60–120 seconds per episode with a hook in every single one. I designed a continuous 12-minute piece. **That is the Quibi-shaped mistake** — assuming production continuity is the value when the format's value is the hook density. The right structure is **8 micro-episodes of ~90 seconds inside the 12-minute session**, each with its own cold open and its own cliff.

**3. The reward economy is information, and information isn't a feeling.** "You banked evidence card C2 — paint fleck, grey enamel" is a spreadsheet row. The format's currency is catharsis: *you made him say it out loud, in front of her.* We built a knowledge economy where the genre runs an emotion economy.

**4. The stakes are professional, not personal.** "An innocent man will be arrested" is an abstraction about justice. Microdrama stakes are about a specific person who wronged you and will be made to know it. There is nobody in v0.1 to hate.

**5. One register for seven days.** No 泪点, no 磕点, no 燃点 — no tear beat, no relationship beat, no hype beat. Writers' rooms score every episode against that checklist. Ours would score 1/6.

**6. The gestures are physics, not feeling.** Turn a dial. Hold a torch. Sweep a light. These are *tasks*. In the vertical frame — which exists for **faces, hands and intimacy** — we spent our interaction budget on a padlock. See §3, which is the most important section here.

**7. The prototype was built for a laptop.** Portrait frame on a desktop page, wheel-to-zoom, mouse-scale hit targets, hover states. You can't test a thumb format with a mouse.

---

## 3. The fix that matters most: make the gesture carry the drama

This is the single most valuable change in the redesign, and it costs nothing to make.

**The input primitives all survive. The fiction of each one changes from a task to a feeling.**

| v0.1 — a task | v0.2 — the same input, doing dramatic work |
|---|---|
| **Steady** — hold the torch on the rail | **Don't look away** — hold your eyes on the boy while everything in frame invites you to look elsewhere |
| **Peel** — lift a print inside a tolerance band | **Kneel** — get down to a child's eye level, too fast and he flinches, too slow and the moment's gone |
| **Swipe** — answer the phone | **Tear it** — rip the closure report in half across the DCP's desk |
| **Turn** — a padlock dial | **Turn her face to the light** — so she has to be looked at |
| **Press** — a pressure meter | **Push him** — one word too far and he lawyers up |
| **Sweep** — a torch across a floor | **Search her face** — find the tell before she reassembles it |
| **Hold** — do nothing | **Hold** — say nothing while she breaks. *Unchanged, and now it's the best beat in the game.* |

Same code. Same tuning knobs. Same library. Entirely different product. Every beat now has a person in it and an emotional consequence, which is what a vertical frame is for.

**The rule going forward:** a beat that could be performed on an object with nobody present is a beat we shouldn't ship. If there's no face in the frame, it isn't a microdrama beat.

---

## 4. Revised episode architecture

**One session = 12 minutes = 8 micro-episodes.** Each micro-episode:

| Window | Beat |
|---|---|
| 0:00–0:03 | **Golden hook** — mid-conflict. Never establishing. One interaction inside the first 3 seconds. |
| 0:03–0:12 | Conflict, relationship, objective. 1–2 interactions. |
| 0:12–0:35 | **First 爽点** — a compressed payoff, witnessed. |
| 0:35–1:15 | Escalation. Emotional checkpoint every 20–30s. 3–4 interactions. |
| 1:15–1:30 | **Cliffhanger** — Revelation, Reversal, Deadline or Intrusion. Often the HOLD beat. |

**8–10 interactions per micro-episode × 8 = 64–80 per session.** That is well above your 24–48 minimum, and it is the density the format actually runs at. The v0.1 figure of 34 was calibrated to a game, not to this.

Between micro-episodes: a **1.5-second title card** with the next episode number and a one-line hook. Not a menu. Not a summary. The cut is the product.

**Keep:** the 1 real second = 2 drama minutes ratio, the 7-day arc, the daily notification, the 90-minute start window. Those all still hold.

---

## 5. What survives from v0.1 — and is now better supported

- **No fail states.** Strongly validated. 90%+ of microdrama viewers exit at the first hard friction point. A dead end would be fatal.
- **Gestures instead of choices.** This is the most defensible decision in the whole project and the research strengthens it enormously: a gesture doesn't fork the video, so there is **zero branching waste** — the economics that killed Bandersnatch, the 2019 Chinese wave and ByteDance's 2024 attempt simply don't apply. And at one input every 15–20 seconds we're inside the flow threshold that a choice-every-four-minutes format can never reach.
- **The ~18-second cadence** matches Jack Attridge's *Erica* rule (something to do every 15–20 seconds) almost exactly. v0.2 tightens it to ~10–12s for hook episodes.
- **Three-tier outcomes.** Keep the mechanic, change what it pays out — catharsis, not clues.
- **Anti-repetition rules and the verb library.** Keep entirely. Reskin the fiction, not the code.
- **Owning our own client.** Netflix's stated reason for killing interactive was platform tech debt across every device it supports. We ship inside one app we control. That whole failure mode is off the table for us.

---

## 6. The v0.2 prototype — what it demonstrates

`prototype/seven-rains-v2.html` is Episode 1's first ~100 seconds, rebuilt to the rules above. Open it on a phone.

**The scene:** Vidya is being made to sign the closure report that hangs Salim. The boy is on the floor outside the glass. She signs it — then tears it. Then she goes down to the kid's eye level in the corridor, and he hands her a crayon drawing of a person in a yellow raincoat and says *"Appa said you'd come."*

**The beats, and the rule each one demonstrates:**

| # | ~t | Beat | Demonstrates |
|---|---|---|---|
| 1 | 0:02 | **Push it back** | Golden hook — an interaction inside 3 seconds, mid-conflict, before any name is known |
| 2 | 0:10 | **Don't look away** | Conflict + relationship + objective established; a hold beat with a face in it |
| 3 | 0:24 | **Tear it** | The first 爽点 — defiance, compressed, witnessed by the antagonist |
| 4 | 0:38 | **Push through** | Escalation; traversal that is still about people |
| 5 | 0:47 | **Catch it** | Emotional checkpoint; reflex beat |
| 6 | 0:58 | **Kneel** | 泪点 — tolerance-band drag where too fast reads as brusque |
| 7 | 1:10 | **Unfold it** | Intimacy; hands in frame |
| 8 | 1:18 | **Look closer** | The reveal — the drawing is of a woman in a yellow raincoat |
| 9 | 1:27 | **Hold** | Cliffhanger + the restraint verb. Hold and you see who's watching. Tap and you miss her. |

**The buried payoff:** a nine-year-old hands the player the answer to the entire case in Episode 1, and only the player who holds still at the last beat sees the face. That is the format's own logic — instant gratification on the surface, a long game underneath.

**On the look:** the prototype renders as a vertical animatic — lit figures, camera pushes, cut-on-beat, burned-in subtitles. In production every frame is a live-action plate. Two things worth noting from the research: microdrama is watched **sound-off in bed by ~70% of viewers**, so burned-in subtitles aren't a fallback, they're the primary channel; and the vertical frame wants **faces, hands and intimacy** — *"two people arguing at a kitchen table works far better than a wide stadium shot"* — which is also, conveniently, the cheapest thing to shoot.

---

## 7. What I'd want to learn from the first test

Not "did people interact." They will — 94% did on Bandersnatch, 97.4% on 《爱情公寓5》, and both categories died anyway. **Interaction rate is table stakes and predicts nothing.**

What actually matters, in order:

1. **Do they come back on Day 2 without a reward prompt?** The only question that matters in week one.
2. **Where in the 100 seconds do they stop?** Cluster the drop-offs. A spike at a beat is a broken beat, not a bored player.
3. **Does the HOLD beat read?** If under 30% hold on first encounter, it needs a diegetic teacher — one line, once, and never again.
4. **Does the event move parent-game DAU and session length on non-event days?** If it doesn't, the drama was a hobby.
5. **Per-beat tier distribution.** MISSED above ~25% means mistuned. CLEAN above ~90% means the beat is free and should be cut or tightened.
