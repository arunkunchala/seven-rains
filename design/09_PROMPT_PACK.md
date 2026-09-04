# Generated 2D — production art pipeline
### Project K · The Last Drop

The engine now reads **art slots**. Drop a file at the path in `art/manifest.json` and that panel upgrades; miss one and it falls back to the greybox SVG. Nothing breaks while art is in flight, and no code changes when it lands.

---

## 1. The only thing that actually decides quality

Not the prompt. **Character consistency.** 67% of practitioners name it as the number one production obstacle, and it is the difference between "AI slop" and "a game". The protocol below exists to solve exactly that, and it must be followed in order.

### The order of operations

```
1. Style probe        →  lock ONE style string. Never edit it again.
2. Character sheets   →  6 characters × 5 plates each, generated FIRST.
3. Environment plates →  8 environments, EMPTY of characters.
4. Shot composites    →  character cut-outs over plates, in-engine.
```

**Do not generate characters inside scenes.** Generate the world empty and the people separately, then composite. This is §12 of the build spec and it is the single highest-leverage decision in the pipeline, because it decouples "does this character look the same" from "does this scene look right". Fixing a bad scene no longer risks the face.

### Locked style string — append to every prompt, unchanged

```
cinematic key art, sun-blasted wasteland, hard low-angle sunlight with cool
sky bounce fill, heavy atmospheric haze, dust in the air, weathered scavenged
metal and patched cloth, muted dust-ochre and charcoal palette, teal only on
technology, warning red only on Complex hardware, painterly rendered
illustration, strong readable silhouette, shallow depth of field,
volumetric light shafts, film grain, no text, no watermark
```

### Locked negative prompt

```
text, letters, watermark, signature, logo, UI, interface, HUD, subtitles,
green foliage, plants, grass, vegetation, lens flare artifacts, extra fingers,
extra limbs, deformed hands, changing costume, inconsistent jewellery,
plastic skin, oversaturated, neon, cyberpunk magenta, anime, chibi, 3d render,
cgi, low detail background, cluttered composition
```

⚠️ **`green foliage, plants, grass, vegetation` is in the negative for a reason.** The archive's green is the episode's strongest visual moment and the spec forbids spending it early. Only remove those four terms for cards **S06-02 onward**.

### Palette — give the generator the actual values

| Role | Hex |
|---|---|
| Sky high / thin air | `#6E93AE` |
| Sky horizon haze | `#E8C89A` |
| Sun core / bloom | `#FFF6DE` / `#FFCE7A` |
| Far ridge | `#A98A66` |
| Mid ground | `#6E5236` |
| Near ground / shadow | `#33220F` → `#120B05` |
| Skin lit / shadow | `#EFC38A` → `#33190A` |
| Cloth | `#7A6A52` → `#3A3126` |
| Weathered metal | `#D6CFBE` → `#4A453C` |
| Rust | `#9E5227` |
| Technology (teal) | `#3FA5A8` |
| Complex warning (red) | `#E04B32` |
| **Archive green — S06-02 ONLY** | `#4BE07A` |

### Consistency mechanics

- **Reference conditioning on every shot.** Whatever the tool calls it — image prompt, `--cref`, IP-Adapter, reference-only ControlNet — feed the character sheet in at 0.6–0.8 weight. Text alone is not a likeness pipeline; the spec says so explicitly.
- **One seed family per character.** Record it in `art/ref/SEEDS.md`. Vary the shot, not the seed.
- **Train a LoRA if the budget allows.** 20–30 approved images per hero character beats any amount of prompt engineering, and it is the only thing that survives across a 26-card episode.
- **Reject aggressively.** Altered face, changed costume seams, drifting jewellery, inconsistent weapon geometry, extra fingers — regenerate rather than retouch. The spec lists these as hard rejects.
- **Human art-direction pass on everything.** Non-negotiable per §12, and per the IP guardrails below.

---

## 2. ⚠️ Before any of this runs

The spec is unambiguous and it is worth repeating at the top of the pipeline, not the bottom:

> *"Use approved reference packs as image conditioning or direct assets when contractually permitted."*
> *"Never synthesize or approximate protected actor likenesses as final assets."*

So: **do not prompt for Prabhas, Amitabh Bachchan, or any actor by name, description or lookalike.** Do not prompt for Bujji's design. The character sheets below describe *original* wasteland archetypes that hold the shot composition. When approved likeness packs arrive, they replace the sheets and everything downstream regenerates against them. Until then this pipeline produces a look-and-feel target, not final assets.

---

## 3. Character reference sheets — generate these first

Five plates each, **1024×1024**, flat neutral background, even light. These are references, not shots.

| Plate | Framing |
|---|---|
| A | Front, neutral expression, shoulders up |
| B | Three-quarter left, neutral |
| C | Profile |
| D | Front, in-character expression (per character below) |
| E | Full figure, T-ish stance, showing costume and gear |

**HUNTER** — `art/ref/hunter/`
> Original character, male bounty hunter, late 30s, South Asian, weathered sun-damaged skin, heavy brow, deep-set hooded eyes, strong cut jaw, dark matted hair pulled back into a topknot with loose strands, full dark beard, faint scar across the right temple, dust on the face. Costume: scavenged asymmetric shoulder plate on the left, layered charcoal and olive cloth, cracked leather bandolier strap across the chest, rusted buckles, fingerless wraps. Expression plate D: dry amused smirk.

**CARRIER** — `art/ref/carrier/`
> Original character, young scavenger, roughly 16, slight fast-looking build, South Asian, dust-caked face, sun-bleached head wrap in faded ochre cloth, improvised leather-and-glass goggles pushed onto the brow with visible strap wear, worn satchel on a heavy strap. Expression plate D: wary, chin up, not frightened.

**GIANT** — `art/ref/giant/`
> Original character, ancient warrior, immense scale, long white-grey hair and full beard, weathered aged face, layered ancient armour far older than the surrounding technology, heavy shoulder plates, long dark cloak, tall staff with a worn metal head. Frame from a low angle. Expression plate D: absolute calm, unhurried.

**BROKER** — `art/ref/broker/`
> Original character, black-market fixer, 50s, hooded cloth head wrap, industrial half-mask respirator over nose and mouth with a circular filter, only the eyes visible, layered trader's robes with hidden pockets. Expression plate D: eyes narrowed, calculating.

**OFFICER** — `art/ref/officer/`
> Original character, institutional officer in a clean powered exoskeleton, field-worn white and black ceramic plating, full helmet with a dark visor and a single horizontal red targeting light, face not visible. Disciplined posture. Cleaner geometry than everything around it.

**TROOPER** — `art/ref/trooper/`
> Original character, rank-and-file soldier, same institutional white-black armour but plainer and more battered, dark visor with red light, rifle carried low. Two silhouettes only: rifle unit and close-combat unit.

---

## 4. Environment plates — no characters in frame

Generate empty. Characters composite in afterwards.

| Slot | Size | Prompt |
|---|---|---|
| `descent` | 1024×2112 | Extreme vertical composition looking down from an impossibly vast clean floating structure into a cramped market far below. Top third: pale monumental tiers hazed by distance. Middle: enormous weathered concrete support columns and stacked improvised housing. Bottom third: dark alley market in deep shadow with warm practical lamps, tarpaulin awnings, tangled cables. Shafts of hot light cutting down through dust. |
| `market` | 1024×1024 | Cramped black-market alley beneath a colossal overhang. Improvised stalls with rust-coloured awnings, hanging cables, smoke, warm dirty practical lamps, barter tech on crates. Deep shadow, single warm key from the left. |
| `holo` | 1024×2112 | Dark interior. A single sealed ancient container on a low metal plinth, lit from below by cold teal projection light. Faint horizontal scan lines in the air around it. Dust motes. Everything else falls into blackness. |
| `contract` | 1024×1024 | Close on a floating translucent contract panel glowing cold teal in a dark room, rows of unreadable glyph-like marks, one large amber confirmation bar across the lower third. Warm rim on a hand entering frame bottom. |
| `highway` | 1024×2112 | Broken elevated highway running to a hazy vanishing point across a dried riverbed. Cracked asphalt, faded centre line, half-buried vehicle wrecks, dunes encroaching from both sides. Low hard sun near the horizon, heavy heat shimmer, distant clean towers barely visible through dust. |
| `overlook` | 896×1024 | High vantage looking down into a ruined settlement at midday. Collapsed roofs, improvised repairs, two columns of black smoke rising. Hard sun, long shadows, a foreground rock ledge as a dark occluder along the bottom edge. |
| `roofs` | 1024×2112 | Layered rooftops of a collapsed settlement, narrow gaps between blocks, a rusted hanging sign spanning a gap, cables strung across. Hard directional sun, deep black shadows, dust haze. Composed for a left-to-right chase route. |
| `shaft` | 1024×2112 | Vertical industrial shaft seen from inside. Metal walkways at three levels, one buckled. Brilliant daylight entering from a gap high above in one volumetric shaft, everything else cool and dim. Heavy dust in the light. |
| `chamber` | 1024×1024 | Ancient stone chamber fused with abandoned machinery. A narrow bright opening at the back, the only light source, blowing out to white. Rubble, hanging chains, cool interior. |
| `giantEnter` | 1024×1024 | Low camera looking up a narrow ruin corridor. Blown dust filling the lower frame from a heavy impact. Hot backlight from behind an unseen figure, deep silhouette territory, one tall staff shape at the right edge. No face resolved. |

---

## 5. The 26 cards

For each card: `<environment plate> + <character cut-outs> + <camera note>`. Only the framing changes per card — that is the point of plate-then-composite.

| ID | Plate | Characters (cut-outs) | Camera |
|---|---|---|---|
| S01-01 | descent | hunter (small, lower third) | Vertical descent, hold wide |
| S01-02 | holo | broker (medium) | Two-shot, container centre safe zone |
| S01-03 | contract | hunter hand | Close, thumb-reachable panel |
| S02-01 | highway | — (runner uses 3D) | High three-quarter chase |
| S02-02 | overlook | carrier, 2× trooper (small) | Over-shoulder, snap-zoom on carrier |
| S03-01 | roofs | hunter (mid) | Side tracking through layers |
| S03-02 | shaft | hunter (small) | Forward, compress depth |
| S03-03 | chamber | carrier, hunter | Interior, strap as interaction line |
| S04-01 | giantEnter | giant silhouette | Feet-to-face vertical reveal |
| S05-01→04 | chamber / ruins | hunter, giant | Medium action, giant stays centred |
| S06-01→03 | chamber | all + officer, troopers | Macro inserts on the archive |
| S07-01→03 | combat hall | hunter, giant, carrier | Single flowing combat shot |
| S08-01 | barricade lane | hunter on vehicle | Behind, narrow lane |
| S09-01→03 | arena | hunter, giant, officer | Circular court, exoskeleton dominates upper frame |
| S10-01 | collapsing ruins | all | Alternating vertical climb / lateral beam |
| S11-01 | settlement exterior | hunter, carrier, giant | Quiet, static, eye-level |
| S12-01 | settlement garden | hunter, carrier | Close tactile, **green enters here** |

Cards S04 onward need three more environment plates (**combat hall**, **barricade lane**, **arena**, **settlement garden**) — write them the same way once S01–S03 have proved the look.

---

## 6. Wiring art in

`art/manifest.json` lists every slot, how many times it is used, its primary aspect and the size to generate at. Slots used at two very different aspects are flagged — generate a second variant rather than letting cover-crop eat the composition.

Register art either by editing the `ART` object in `prototype/app.html`, or at runtime:

```js
MicrodramaArt.set('last-drop', {
  descent: 'k/descent.webp',
  holo:    'k/holo.webp'
});
MicrodramaArt.layers('last-drop', {
  descent: [{src:'ch/k/hunter_smirk.webp', x:'50%', y:'86%', w:'46%'}]
});
```

`MicrodramaArt.usage()` prints where every slot is used and at what aspect, so the manifest can be regenerated whenever pages change.

**Format:** WebP, quality ~82. Budget roughly 120–200 KB per full-page plate, 60–110 KB per panel, 40–80 KB per character cut-out (PNG with alpha where a cut-out needs soft edges). A 26-card episode should land under 8 MB of art.

---

## 7. Order of work

1. **Style probe** — generate `highway` six times, pick one, freeze the style string. Half a day.
2. **Character sheets** — 6 × 5 plates. This is where consistency is won or lost. One to two days.
3. **S01–S03 plates** — the ten above. Drop into `art/k/`. One day.
4. **Play it.** The greybox falls away panel by panel as files land, so the whole slice is testable throughout.
5. Only then extend to S04–S12.

The pipeline is designed so step 4 never blocks: an empty `art/` folder is a working build.
