# art/

Drop generated art here. The engine reads `manifest.json`; any file that is
missing or fails to load falls back to the greybox SVG, so an empty folder is
a working build.

```
art/
  manifest.json     every slot, its aspect and the size to generate at
  k/                Project K — The Last Drop, environment plates
  sr/               Seven Rains, environment plates
  ch/k/             Project K character cut-outs (PNG with alpha)
  ref/              character reference sheets + SEEDS.md — NOT shipped
```

`ref/` is the consistency source: generate character sheets first, feed them
back as image conditioning on every shot. See `design/09_PROMPT_PACK.md`.

Register art by editing the `ART` object in `prototype/app.html`, or at
runtime with `MicrodramaArt.set(storyId, {slot:'path.webp'})`.
Run `MicrodramaArt.usage()` in the console to regenerate the manifest data
after changing any page layout.

**No likenesses.** Do not prompt for real actors by name or description.
Everything here is original design until approved reference packs land.
