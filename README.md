# HârnWorld Location Module: Three Brothers Barrow
[![Version (latest)](https://img.shields.io/github/v/release/toastygm/hm-loc-tbb)](https://github.com/toastygm/hm-loc-tbb/releases/latest)
[![Forge Installs](https://img.shields.io/badge/dynamic/json?label=Forge%20Installs&query=package.installs&suffix=%25&url=https%3A%2F%2Fforge-vtt.com%2Fapi%2Fbazaar%2Fpackage%2Fhm-loc-tbb&colorB=4aa94a)](https://forge-vtt.com/bazaar#package=hm-loc-tbb)
[![GitHub downloads (latest)](https://img.shields.io/badge/dynamic/json?label=Downloads@latest&query=assets[?(@.name.includes('zip'))].download_count&url=https://api.github.com/repos/toastygm/hm-loc-tbb/releases/latest&color=green)](https://github.com/toastygm/hm-loc-tbb/releases/latest)

Three Brothers Barrow is a "Location Module" for the Foundry VTT system. It is designed to provide
a ready-made Jarin barrow tomb for heroes to explore, along with several adventure hooks. 
This location module is designed for the [HârnWorld](https://columbiagames.com/harnworld/)
fantasy setting; however, this barrowcould be adapted to exist anywhere in any fantasy setting.

Although designed for use with the [HârnMaster](https://foundryvtt.com/packages/hm3)
system, this module is mostly system-agnostic, with the exception of Actors (a monster).
Detailed descriptions of the actors has been provided in journal entries to facilitate
conversion to other game systems.

# Maps

The original maps from this work have been used.  The following
maps are part of this module.

## General Area

Map of General Area around Three Brothers' Barrow

<img src="assets/scenes/tbb-area.webp" alt="Three Brothers' Barrow Area" width="600"/>

## Cave

<img src="assets/scenes/tbb-cave.webp" alt="Cave" width="600"/>

## Tomb

<img src="assets/scenes/tbb-tomb.webp" alt="Tomb" width="600"/>

# Credits

This module is made possible by the hard work of HârnWorld fans,
and is provided at no cost. This work is an adaptation of the article
[Three Brothers Barrow](https://www.lythia.com/adventures/three-brothers-barrow/) available
at the HârnWorld fan site [Lythia.com](https://www.lythia.com/).

**Writer:** Rob Barnes

**Original Maps:** Rob Barnes

**Artist:** Richard Luschek

**Adapted to Foundry VTT:** Tom Rodriguez

Illustrations by Richard Luschek; visit his Patreon page at https://www.patreon.com/LuschekII.

This module is "[Fanon](https://www.lythia.com/about/publishing-fan-written-material/)",
a derivative work of copyrighted material by Columbia Games Inc. and N. Robin Crossby.


# Development

Requires Node.js >= 24.

## Project structure

- `assets/packs/<name>/unique/` — source JSON files for each compendium pack
- `assets/templates/module.template.json` — module manifest template (version/URLs are injected at build time from `package.json`)
- `scripts/init.js` — ScenePacker integration
- `utils/` — build scripts

## Common tasks

```sh
npm install                  # install dependencies (first time / after pulling)
npm run deploy:qa            # build and deploy to local QA Foundry instance
npm run deploy:release       # build and create build/dist/module.zip
npm run release              # create GitHub release (needs GITHUB_TOKEN)
npm run clean                # remove build/
```

## Making content changes

Edit the JSON files in `assets/packs/<name>/unique/`. These are the source of truth — LevelDB packs are compiled from them at build time.

## Deploying locally for testing

Set environment variables for your Foundry data paths (in `.env.local` or your shell):

```
FOUNDRYVTT_DEV_DATA=/path/to/foundry/dev
FOUNDRYVTT_QA_DATA=/path/to/foundry/qa
FOUNDRYVTT_PROD_DATA=/path/to/foundry/prod
```

Then `npm run deploy:qa` (or `:dev` / `:prod`) will build and rsync to that instance.

## Releasing

1. Bump the version in `package.json`
2. Commit and push to `main`
3. `npm run deploy:release` — builds and creates `build/dist/module.zip`
4. `export GITHUB_TOKEN=$(gh auth token)` (or set in `.env.local`)
5. `npm run release` — creates a GitHub release with `module.zip` and `module.json` attached
