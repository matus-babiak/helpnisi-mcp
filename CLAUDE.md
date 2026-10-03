# Helpnisi web – kontext pre AI agentov

Tento súbor čítaj ako prvý. Platí pre Claude Code, Claude (Cowork/mobil) aj Cursor (cez `AGENTS.md`).

## Čo to je

- Web terapeutky Mgr. Jessicy Sulev (značka **helpnisi**), staviam ho ja – Matúš.
- Beží na WordPresse s Elementorom (editor V4 / atomic prvky) + Elementor Pro (Theme Builder).
- Vývojová adresa: https://helpnisi.matusbabiak.sk
- **Obsah webu nie je v tomto repozitári.** Stránky žijú vo WordPresse a upravujú sa cez MCP server Elementoru `template-elementor`. Repozitár drží podklady (obrázky), konfiguráciu MCP a tieto pravidlá.

## Pripojenie (MCP)

- Server: `https://helpnisi.matusbabiak.sk/wp-json/elementor/mcp/`
- Prihlásenie: HTTP Basic, hodnota sa berie z premennej prostredia `HELPNISI_MCP_AUTH` (pozri `README.md`).
- Heslá ani base64 reťazec **nikdy** nezapisuj do súborov v repozitári – repo je verejné.

## Dokumenty vo WordPresse

| Čo | ID | Poznámka |
|---|---|---|
| Domovská stránka „Domov" | 19 | šablóna stránky `elementor_header_footer` |
| Hlavička „Helpnisi – Header" | 79 | Theme Builder, podmienka `include/general` |
| Pätička „Helpnisi – Footer" | 80 | Theme Builder, podmienka `include/general` |

Sekcie domovskej stránky v poradí: Hero, Problems, Main Idea, Whole, Approach, Methods, Expertise, Start, Trust, Contact, Support, Reviews.

## Pravidlá dizajnu

- **Šírka obsahu 1140 px.** Každá sekcia má dve vrstvy:
  1. vonkajší obal `xxx-section` na celú šírku – nesie pozadie a odsadenia (desktop `4.5rem 3rem`, mobil `3rem 1.25rem`),
  2. vnútorný kontajner – `width: 100%; max-width: 1140px; padding: 0`, vycentrovaný.
  Nové sekcie stavaj rovnako.
- Farby: tmavozelená `#01372F`, terakota `#C27559`, svetlá broskyňová `#FFE9E1`, krémová `#FFFBF5`, ružová `#FCD9CE` / `#E3B0A3`.
- Písma: nadpisy `DM Serif Display`, text `Inter`.
- Tlačidlá: pilulky (`border-radius: 9999px`), hlavné zelené, vedľajšie obrysové.
- Animácie len veľmi jemné. Žiadne pomalé posuny prvkov s textom (sekajú). Tiene čo najjemnejšie.
- Texty na webe sú od klientky – nemeň ich bez pokynu.

## Hero sekcia (stránka 19)

- Pozadie: `linear-gradient(105deg, #FFF8F4, #FFE9E1 50%, #FAD3C6)`.
- Vľavo: štítok „Psycho • Bio • Socio • Spirituálno", H1, tri odseky, dve tlačidlá.
- Vpravo: fotka vložená do oblúka (`overflow: hidden`, horné rohy zaoblené), okolo tenký obrys, hviezdička, bodka, biela kartička s menom.
- Fotka: `images/jessica-sulev-helpnisi-portrait-stol.png` (výrez so stolom, v Médiách ID 72).
- Animácie: postupný nábeh textov pri načítaní, pulzujúca hviezdička, pohupujúca sa bodka, pomaly sa posúvajúci svetlý kruh. Kartička s menom sa nehýbe.

## Hlavička (79)

- Sticky cez vlastné CSS šablóny (`selector { position: sticky; top: 0; z-index: 999; }` + posun pod admin lištu).
- Polopriehľadné pozadie s `backdrop-filter: blur(14px)`, tieň `0 6px 24px -10px rgba(194,117,89,0.12)`.
- Položky menu sú zatiaľ texty bez odkazov.

## Ako pracovať s MCP Elementoru (overené pasce)

1. **Zmeny sa ukladajú do konceptu.** Po `manage-elements` / `build-composition` / `update-page-settings` zavolaj `publish-document`, inak zmena nie je naživo.
2. **Publikuj po každom kroku**, najmä medzi `build-composition` a `manage-elements`. Inak ďalší nástroj číta starý strom a prepíše predošlú zmenu.
3. **Po publikovaní vyčisti cache Elementoru** (Elementor → Nástroje → Clear Files & Data). Bez toho živá stránka ukazuje starý HTML/CSS.
4. `get-page-structure` číta publikovanú verziu, nie koncept.
5. **Padding:** nemiešaj `max()` / `calc()` s bežnými hodnotami v jednom `padding` – zvislé odsadenia sa stratia. Šírku obsahu rieš vnútorným kontajnerom.
6. Absolútne pozicované prvky dostávajú šírku 100 % – vždy nastav `width` ručne.
7. `radial-gradient` parser neprijme, `linear-gradient` áno. `backdrop-filter`, `box-shadow`, `transition`, `&:hover`, `aspect-ratio` fungujú.
8. Obrázok sa nastavuje ako `{"image": {"src": {"id": <ID média>, "alt": "…"}, "size": "full"}}`.
9. MCP nevie nahrávať súbory do Médií – nahraj ich cez WP admin a potom ich nájdi cez `list-assets`.
10. Animácia `fade` môže prepísať `opacity` prvku na 1 – nedávaj ju na prvky so zníženou priehľadnosťou.

## Otvorené veci

- Odkazy v menu a v pätičke (kam majú viesť).
- Kotva `id="kontakt"` je na vonkajšom obale kontaktnej sekcie (`56037d37`); tlačidlá idú na `/#kontakt` / `#kontakt`.
- Formulár na homepage je klasický Elementor Pro Form (`a19f0c2`, `.elementor-form`). E-mailová akcia nie je nastavená.
- Viaceré fotky sú zatiaľ textové zástupné prvky (Whole, Expertise, Trust, Support).
- Portrét v hero má malé rozlíšenie (zdroj 440 px) – vymeniť, keď klientka pošle väčší.
- Mobilné zobrazenie nebolo systematicky skontrolované.
