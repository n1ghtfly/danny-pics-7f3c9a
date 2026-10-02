# Danny — badge pictures

Source images for the **Thanks Danny** AMOLED badge slideshow, served as a static
GitHub Pages site. The badge fetches `manifest.json`, then downloads each JPEG into its
own LittleFS cache and shows them at random with a slide transition.

## Why it looks the way it does

- **Baseline JPEG only.** The badge's decoder (`TJpg_Decoder`) cannot read progressive
  JPEGs — it fails silently and draws black. `tools/prep_github_pics.py` in the badge
  project re-encodes everything as baseline and proves it on read-back.
- **Sized for a round 466×466 panel.** The short side is scaled to 466 and the long side
  capped at 1100, so landscape pictures stay wider than the panel and the badge can slide
  across them rather than showing a letterboxed strip.
- **No index linking.** The site is public (free GitHub Pages requires a public repo) but
  carries `noindex,nofollow` and is not linked from anywhere, so it is effectively
  unlisted. The repo name is deliberately unguessable.

## Adding pictures

1. Drop the originals into the badge project's `pics` source folder.
2. Run the prep tool — it renumbers, re-encodes and rewrites `manifest.json`:

       python tools/prep_github_pics.py

3. Copy the results here and commit. The badge picks up the new set on its next refresh.

## Files

| File | Purpose |
|---|---|
| `manifest.json` | Written by the prep tool: panel size, picture count, and each file's name, dimensions and byte size |
| `pNN.jpg` | The prepped pictures, in a stable numbered order |
| `index.html` | Browsable contact sheet (reads the manifest; nothing to edit when pictures change) |
