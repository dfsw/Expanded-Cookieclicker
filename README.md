# Cookie Clicker + Just Natural Expansion (standalone mirror)

A static mirror of Cookie Clicker (v2.058, mirrored from orteil.dashnet.org) that
auto-loads the [Just Natural Expansion](https://github.com/dfsw/Just-Natural-Expansion)
mod at startup - no console, bookmarklet, or extension needed.

Built by `tools/build_standalone.sh` in the JNE repo. Do not edit by hand;
re-run the script to rebuild.

## Deploy to GitHub Pages

```bash
cd standalone
git init -b main
git add -A
git commit -m "Cookie Clicker + JNE standalone"
git remote add origin https://github.com/<user>/<repo>.git
git push -u origin main
```

Then: repo Settings → Pages → Source = "Deploy from a branch" → main / root.
Site appears at `https://<user>.github.io/<repo>/`.

The same folder also drops onto Cloudflare Pages, Netlify, or itch.io
(zip-upload) - deploying to multiple hosts is a cheap hedge against
school/work filters blocking any one domain.

## How it works

- `index.html` is the vanilla shell with `PRESETMODS=['...JustNaturalExpansion.js']`;
  `main.js` loads it during launch, identical to `Game.LoadMod`.
- `Game.resPath='./'` is set after `main.js` so the mod's `resPath` fallbacks
  resolve to local copies of vanilla assets.
- All mod files (data.js, minigames, sprite sheet, puzzle packs) load remotely
  from jsdelivr/GitHub, same as the normal install paths - updating the mod
  repo updates what players get, no redeploy needed.
- Orteil's ad/analytics code is left intact.

## Caveats

- Saves are per-origin: players start fresh here and can export/import via
  Options. On managed devices (e.g. Chromebooks) localStorage may be wiped on
  sign-out - tell players to export saves.
- A few mod images/audio still reference orteil.dashnet.org directly; on
  networks that block that domain entirely those degrade (mod itself still
  loads). Bundling the mod locally would fix this if ever needed.
- Vanilla updates require re-running the build script.
- The game is copyright Orteil - the source itself asks not to be re-hosted.
  Keep this unlisted/private-ish and don't monetize it.
