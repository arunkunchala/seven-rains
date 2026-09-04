# Interactive Microdrama — POC

**Series:** Seven Rains · **Case One:** The Glasshouse
Contemporary Bengaluru detective serial. 7 daily episodes, 12 real minutes each, 1 real second = 2 drama minutes.

## Contents

| Path | What it is |
|---|---|
| `design/01_STORY_BIBLE.md` | The case: victim, six suspects, the real solution, the day-by-day clue chain, the Day 7 accusation and its four endings |
| `design/02_INTERACTION_SYSTEM.md` | 20 gesture verbs in 5 classes, the time/penalty model, three-tier outcomes, anti-repetition rules, difficulty curve, the 12-minute episode template |
| `design/03_EVENT_AND_RETENTION.md` | Live-event window, miss-a-day catch-up, the Case Board, streaks, notification copy, instrumentation, production load |
| `design/04_MARKET_CONTEXT.md` | **Research briefing** — how the microdrama business actually works, the craft rules, the interactive-drama graveyard and why it died, and the six conclusions for us |
| `design/05_V02_REDESIGN.md` | **Honest audit of v0.1** and the v0.2 redesign — why a detective story is the wrong genre shape, and the gesture reskin that fixes it |
| `design/06_EPISODE_PACING.md` | **The 12-minute structure** — comic pages × hypercasual mini-games, density rules, the Issue 1 pacing map, the mini-game library |
| `prototype/seven-rains-v3.html` | **v0.3 — the current prototype.** Comic-book panels with guided-view reading, a Subway-Surfers-style lane runner, spot-the-clue, timing/swipe/hold QTEs. Sequence 1 of 4 (~3½ min). Open on a phone. |
| `prototype/seven-rains-v2.html` | v0.2 — animatic style, kept for reference |
| `prototype/seven-rains-demo.html` | v0.1 — gesture testbed, kept for reference |

## The three decisions everything else hangs off

1. **You cannot fail into a dead end.** Every interaction resolves CLEAN / ROUGH / MISSED and the scene continues regardless. Sloppy play costs you *knowledge*, never playtime — which is what makes a fixed 12-minute daily event survivable.
2. **The accusation is an assembly task, not a multiple-choice question.** Day 7 asks the player to chain evidence cards they actually earned. No "pick the killer" menu.
3. **The gesture library is the product.** ~240 authored interactions per case only becomes affordable if they are 240 tunable data rows over 20 reusable verbs, with a build-time linter enforcing the anti-repetition rules.

## The thing to decide next

The genre. A murder mystery is a **deferred-gratification** form; microdrama is a **compressed-gratification** form, and they pull against each other. `05_V02_REDESIGN.md` §1 lays out three ways to resolve it. Recommendation: keep the case as the plot and put a personal antagonist engine underneath it, so every episode pays something off inside its own 90 seconds.

## Status
v0.3 — the format is now a comic-book story engine with hypercasual mini-games as the action beats. Sequence 1 of Issue 1 is playable on a phone; sequences 2–4 are mapped in `06_EPISODE_PACING.md` and not yet built.
