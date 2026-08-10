# Cesta Prstenu 💍

Interaktivní průvodce **Společenstvem Prstenu** pro předčítání dětem (český překlad). Postavené pro předčítání Pána prstenů dvěma syny.

➡️ Otevři **`stredozem.html`** v prohlížeči (funguje offline, je to jeden soubor).

## Co appka umí

- 🗺️ **Mapa cesty** — vyznačená trasa Společenstva + lišta zastávek; v dětském režimu bez spoilerů (odemyká se, jak čtete).
- 🧙 **Postavy** — malované portréty s deníkem „příběh zatím" a s výslovností jmen.
- 🖼️ **Ilustrace ke každé kapitole** — malovaná scéna klíčového momentu + popisek.
- 📖 **Kapitoly** — režim *Táta* (shrnutí, na co se zaměřit, otázky, „metr strašidelnosti", slovíčka) i režim *Kluci* (shrnutí „co se stalo" + kvízy, vše bez spoilerů).
- 🌍 **Svět a Vztahy** — co je Jeden prsten, kdo je Sauron, rasy Středozemě, časová osa a kdo s kým souvisí (v režimu Kluci se odkrývá postupně, aby to neprozradilo děj).
- 🌗 **Světlý / tmavý motiv** — přepínač v hlavičce; bez volby se řídí nastavením systému.

## Struktura projektu

- `stredozem.html` — **sestavená appka** (jeden soubor, obrázky vložené uvnitř). Tohle se otevírá a sdílí.
- `stredozem.template.html` — **zdrojová šablona** (HTML/CSS/JS). Tady se edituje.
- `assets/` — obrázky, které se při sestavení vkládají do appky:
  - `map.jpg` — mapa Středozemě (optimalizovaná, vstup buildu),
  - `portraits/<id>.jpg` — portréty postav (`id` = např. `frodo`, `gandalf`, `stara-vrba`),
  - `scenes/<n>.jpg` — ilustrace kapitol `1`–`22`.
- `build.mjs` — sestavovací skript (Node).
- `mapa-stredozem-original.jpg` — původní mapa ve vysokém rozlišení (10000×5455). **Není součástí repa** — drží se jen lokálně (mimo git). Build ji nepotřebuje, používá optimalizovanou `assets/map.jpg`.

## Sestavení

Po úpravě šablony nebo obrázků spusť:

```bash
node build.mjs
```

Skript vezme `stredozem.template.html`, nahradí tokeny za obrázky z `assets/` (jako base64 data URI) a zapíše `stredozem.html`:

| token | zdroj |
| --- | --- |
| `__MAP_DATA_URI__` | `assets/map.jpg` |
| `__IMG_<id>__` | `assets/portraits/<id>.jpg` |
| `__SCENE_<n>__` | `assets/scenes/<n>.jpg` |

Seznam tokenů se čte přímo ze šablony a build skončí chybou, pokud některý zůstane nenahrazený nebo chybí obrázek — takže se nedá omylem vydat rozbitý soubor.

## Poznámky

Jména postav vycházejí z překladu **Stanislavy Pošustové** (Pytlík, Křepelka, Hůrka, Roklinka, Chodec…). Pár jmen si nejsem 100% jistý (sedlák Maggot, Ječmínek Máselník, Zlatěnka) — když se liší od tvého vydání, dají se snadno sladit. Mapa má popisky anglicky, české názvy jsou u pečetí.
