# Helpnisi web – vstup pre AI agentov

**Zdroj pravdy pre vývoj:** [`docs/ai/README.md`](docs/ai/README.md).  
Tento súbor je krátky operatívny vstup a zoznam overených MCP pascí. Produkt, mapa obsahu, konflikty so starými poznámkami a workflow plán/implementácia sú v `docs/ai/`.

Platí pre Claude Code, Claude (Cowork/mobil) aj Cursor (`AGENTS.md`, príkazy `/helpnisi-plan` a `/helpnisi-implement`).

## Čo to je

- Web terapeutky Mgr. Jessicy Sulev (značka **helpnisi**), stavia ho Matúš.
- WordPress + Elementor V4 (atomic) + Elementor Pro Theme Builder.
- Vývojová adresa: https://helpnisi.matusbabiak.sk
- **Obsah webu nie je v tomto gite.** Stránky sa upravujú cez MCP `template-elementor`. Repo drží podklady, MCP konfiguráciu, knowledge base a tieto pravidlá.

Zmenu webu najprv plánuj (`/helpnisi-plan`). Až po schválení implementuj (`/helpnisi-implement`). V jednom kole jedna **hlavná priorita**.

## Pripojenie (MCP)

- Server: `https://helpnisi.matusbabiak.sk/wp-json/elementor/mcp/`
- Auth: HTTP Basic, hodnota z `HELPNISI_MCP_AUTH` (pozri `README.md`).
- Heslá ani base64 **nikdy** do súborov v repozitári – repo je verejné.

## Dokumenty vo WordPresse

| Čo | ID | Poznámka |
|---|---|---|
| Domovská stránka „Domov" | 19 | šablóna `elementor_header_footer` |
| Hlavička „Helpnisi – Header" | 79 | Theme Builder, `include/general` |
| Pätička „Helpnisi – Footer" | 80 | Theme Builder, `include/general` |

Sekcie domova v poradí: Hero, Problems, Main Idea, Whole, Approach, Methods, Expertise, Start, Trust, Contact, Support, Reviews. Aktuálny stav každej: [`docs/ai/content-map.md`](docs/ai/content-map.md).

## Pravidlá dizajnu

- **Šírka obsahu 1140 px.** Každá nová sekcia: vonkajší obal (pozadie, desktop `4.5rem 3rem`, mobil `3rem 1.25rem`) + vnútorný kontajner `width: 100%; max-width: 1140px; padding: 0`.
- Farby: `#01372F`, `#C27559`, `#FFE9E1`, `#FFFBF5`, `#FCD9CE` / `#E3B0A3`.
- Písma: nadpisy `DM Serif Display`, text `Inter`.
- Tlačidlá: pilulky (`border-radius: 9999px`), hlavné zelené, vedľajšie obrysové.
- Animácie len veľmi jemné. Žiadne pomalé posuny textových blokov. Tiene jemné.
- Texty na webe sú od klientky – nemeň ich bez pokynu.

Viac: [`docs/ai/ui-ux.md`](docs/ai/ui-ux.md), [`docs/ai/business-rules.md`](docs/ai/business-rules.md).

## Ako pracovať s MCP Elementoru (overené pasce)

1. **Zmeny sa ukladajú do konceptu.** Po `manage-elements` / `build-composition` / `update-page-settings` zavolaj `publish-document`, inak zmena nie je naživo.
2. **Publikuj po každom kroku**, najmä medzi `build-composition` a `manage-elements`. Inak ďalší nástroj číta starý strom a prepíše predošlú zmenu.
3. **Po publikovaní vyčisti cache Elementoru** (Elementor → Nástroje → Clear Files & Data). Bez toho živá stránka ukazuje starý HTML/CSS.
4. `get-page-structure` číta publikovanú verziu, nie koncept.
5. **Padding:** nemiešaj `max()` / `calc()` s bežnými hodnotami v jednom `padding` – zvislé odsadenia sa stratia. Šírku obsahu rieš vnútorným kontajnerom.
6. Absolútne pozicované prvky dostávajú šírku 100 % – vždy nastav `width` ručne.
7. `radial-gradient` parser neprijme, `linear-gradient` áno. `backdrop-filter`, `box-shadow`, `transition`, `&:hover`, `aspect-ratio` fungujú.
8. Obrázok: `{"image": {"src": {"id": <ID média>, "alt": "…"}, "size": "full"}}`.
9. MCP nevie nahrávať súbory do Médií – nahraj ich cez WP admin a nájdi cez `list-assets`.
10. Animácia `fade` môže prepísať `opacity` – nedávaj ju na prvky so zníženou priehľadnosťou.

## Otvorené veci

Živý zoznam je v [`docs/ai/content-map.md`](docs/ai/content-map.md). Staršie tvrdenia z tohto súboru (napr. hero 440 px) sú v [`docs/ai/analysis.md`](docs/ai/analysis.md) — neopakuj ich ako aktuálny fakt bez overenia.
