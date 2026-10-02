# UI a UX

Overené z publikovaného CSS stránky 19, headeru 79, footera 80 a z `CLAUDE.md`. Kde sa dohoda v dokumentácii nenašla v CSS, je to povedané.

## Rozloženie

- **Šírka obsahu: 1140 px.** V CSS headeru, footera aj homepage je `max-width:1140px`.
- Sekcia = dve vrstvy:
  1. vonkajší obal na celú šírku — pozadie + padding
  2. vnútorný kontajner `width: 100%; max-width: 1140px; padding: 0`, vycentrovaný
- Desktop padding vonkajšku (dohoda): `4.5rem 3rem`. V CSS homepage je `4.5rem` na viacerých blokoch.
- Mobil padding (dohoda): `3rem 1.25rem`. V mobile CSS homepage sa `3rem` na padding-block-start vyskytuje; `1.25rem` je na headeri.
- Breakpoint, ktorý Elementor používa v týchto súboroch: **767 px**.

Novú sekciu nestavaj na plnú šírku bez vnútorného 1140 kontajnera.

## Farby (v publikovanom CSS homepage)

| Úloha | Hex | Overené |
|---|---|---|
| Tmavozelená | `#01372F` | áno, texty aj primárne tlačidlá |
| Terakota | `#C27559` | áno, hover, akcenty |
| Svetlá broskyňová | `#FFE9E1` | áno |
| Krémová | `#FFFBF5` | áno |
| Ružová | `#FCD9CE` | áno, aj pozadie pätičky |
| Ružová tmavšia | `#E3B0A3` | áno, zriedkavo |
| Hero gradient | `#FFF8F4` → `#FFE9E1` → `#FAD3C6` | farby sú v CSS; presný `linear-gradient(105deg, …)` je v `CLAUDE.md` |
| Header podklad | `rgba(255, 241, 235, 0.86)` | áno |
| Footer text | `#323232` / `#000000` | áno |

Do palety nepridávaj novú výraznú farbu, kým to nie je zadanie.

## Písmo

- Nadpisy: **DM Serif Display**
- Text a menu: **Inter**
- V HTML sa nahrávajú aj Roboto a Roboto Slab (typický Elementor default). **Nové prvky nimi nestyľuj.**

## Tlačidlá

- Tvar: pilulka, `border-radius: 9999px` (v CSS header aj homepage).
- Hlavné: zelené `#01372F`, biely text, jemný zelený tieň; hover terakota.
- Vedľajšie: obrysové (dohoda v `CLAUDE.md`).
- Text tlačidla nemeň bez pokynu.

## Hlavička

- Sticky: custom CSS `.elementor-79 { position: sticky; top: 0; z-index: 999; }` + posun pod WP admin bar.
- `backdrop-filter: blur(14px)`
- Tieň: `0px 6px 24px -10px rgba(194, 117, 89, 0.12)` — sedí s `CLAUDE.md`
- Na mobile je rad menu skrytý. Úpravy navigácie musia povedať, čo sa stane pod 767 px.

## Hero (dohoda + čiastočne overené)

- Ľavý stĺpec: štítok, H1, tri odseky, CTA.
- Pravý: fotka v oblúku (`overflow: hidden`, horné rohy zaoblené), tenký obrys, hviezdička, bodka, biela kartička s menom.
- Fotka: médium **72** (`jessica-sulev-helpnisi-portrait-stol.png`, 880×1044).
- Animácie podľa `CLAUDE.md`: nábeh textov, pulz hviezdičky, pohup bodky, pomalý svetlý kruh. **Kartička s menom sa nehýbe.**
- Animáciu `fade` nedávaj na prvky, ktoré majú byť priesvitné.

Tieto detaily hero (oblúk, hviezdička) sú z `CLAUDE.md`. Vo verejnom HTML sa classy `hero-section` nenašli; vizuál treba pri zmene hero overiť naživo, nie len z DOM class names.

## Pohyb a tiene

- Animácie veľmi jemné.
- Žiadne pomalé posuny celých textových blokov (sekajú).
- Tiene čo najjemnejšie — header tieň je referencia.

## Prístupnosť a UX, ktoré už na webe sú

- Skip link „Preskočiť na obsah“ → `#content`
- Hover aj `:focus-visible` na menu a na CTA v headeri (farba / pozadie)
- Formulár: `aria-label` „Homepage konzultácia“, `autocomplete=email` na e-maile
- Alt texty obrázkov sú dnes prázdne — pri vkladaní fotky vyplň alt, nenechaj prázdne „lebo tak to tam bolo“

## Čo UX ešte láme (fakt, nie návrh)

- CTA na `#kontakt` bez cieľa
- Menu a väčšina pätičky bez odkazov
- Menu na mobile skryté
- Placeholdery namiesto fotiek a recenzií
- Title `Template`

Planning Agent to môže spomenúť, keď to súvisí so zadaním. Nemá to začať „opravovať všetko naraz“.
