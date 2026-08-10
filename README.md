# The Ring's Journey 💍

An interactive, read-aloud guide to **The Fellowship of the Ring**, built for reading Tolkien to kids. Bilingual (English + Czech), with a language switcher and more languages easy to add.

➡️ Open **`stredozem.html`** in a browser (works offline — it's a single file).

## What the app does

- 🗺️ **Journey map** — the Fellowship's marked route plus a strip of stops; in Kids mode there are no spoilers (it unlocks as you read).
- 🧙 **Characters** — painted portraits with a "story so far" diary and (in other languages) how to say the names.
- 🖼️ **A chapter illustration** — a painted scene of the key moment, with a caption.
- 📖 **Chapters** — a *Parent* mode (summary, what to look out for, questions, a "scariness meter", vocabulary) and a *Kids* mode ("what happened" recaps + quizzes, all spoiler-free).
- 🌍 **World & Relations** — what the One Ring is, who Sauron is, the peoples of Middle-earth, a timeline, and how everyone is connected.
- 🌍 **Language switcher** (🌐) and 🌗 **light/dark theme** in the header.

## Languages

The app is **English-first**; Czech is an optional alternate, switchable in the header (🌐). Nothing is hard-coded per language:

- **UI strings** live in the `UI = { en, cs }` dictionary, read via `T('key')`.
- **Content** fields are per-field language maps, e.g. `sum: { en: '…', cs: '…' }`, read via `t(field)` (which falls back to English).

To add a language, add its key (e.g. `de`) to the `UI` dictionary and to the content maps. Structural data (chapter order, scariness ratings, map coordinates, quiz answers) is shared across all languages, so it can't drift.

Czech character and place names follow the translation by **Stanislava Pošustová**; English uses Tolkien's original names.

## Project structure

- `stredozem.html` — the **built app** (one file, images inlined). This is what you open and share.
- `stredozem.template.html` — the **source template** (HTML/CSS/JS). Edit here.
- `assets/` — images inlined at build time:
  - `map.jpg` — the map of Middle-earth (optimised, the build input),
  - `portraits/<id>.jpg` — character portraits (`id` = e.g. `frodo`, `gandalf`, `stara-vrba`),
  - `scenes/<n>.jpg` — chapter illustrations `1`–`22`.
- `build.mjs` — the build script (Node).
- `mapa-stredozem-original.jpg` — the original high-res map (10000×5455). **Not in the repo** — kept locally only. The build doesn't need it; it uses the optimised `assets/map.jpg`.

## Build

After editing the template or the images, run:

```bash
node build.mjs
```

The script takes `stredozem.template.html`, replaces the image tokens with the images from `assets/` (as base64 data URIs) and writes `stredozem.html`:

| token | source |
| --- | --- |
| `__MAP_DATA_URI__` | `assets/map.jpg` |
| `__IMG_<id>__` | `assets/portraits/<id>.jpg` |
| `__SCENE_<n>__` | `assets/scenes/<n>.jpg` |

The token list is read straight from the template, and the build fails if any token is left unreplaced or an image is missing — so you can't ship a broken file.
