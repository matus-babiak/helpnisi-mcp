# Audit pôvodnej dokumentácie

Stav k 2. októbru 2026. Pôvodné súbory sa **neprepisovali potichu**. Konflikty sú tu pomenované. Aktuálne fakty pre vývoj sú v ostatných súboroch tejto zložky.

## Čo v projekte bolo

| Súbor | Účel |
|---|---|
| `CLAUDE.md` | Jediný hustý kontext: produkt, ID dokumentov, dizajn, MCP pasce, otvorené veci |
| `AGENTS.md` | Krátky pointer na `CLAUDE.md` |
| `README.md` | Ako nastaviť `HELPNISI_MCP_AUTH` a MCP |
| `.mcp.json` / `.cursor/mcp.json` | URL MCP + env auth |
| `.env.example` | Prázdny vzor auth |
| `images/` | Podklady |

Žiadne `docs/`, žiadne testy, žiadny `package.json`, žiadny `src/`, žiadne Cursor commands.

## Aktuálne (sedí s realitou)

- Web je WordPress + Elementor V4 + Elementor Pro Theme Builder. Overené z HTML a CSS.
- Vývojová URL `helpnisi.matusbabiak.sk`.
- Stránka 19 = Domov, šablóna `elementor_header_footer`. REST to potvrdzuje.
- Header 79 a footer 80 sedia s CSS súbormi `local-79` / `local-80` / `post-79.css`.
- Sticky header, `blur(14px)`, tieň `0 6px 24px -10px rgba(194,117,89,0.12)` — v CSS je.
- Paleta `#01372F`, `#C27559`, `#FFE9E1`, `#FFFBF5`, `#FCD9CE`, `#E3B0A3` — v CSS homepage je.
- 1140 px, Inter, DM Serif Display, pilulky `9999px` — v CSS sú.
- Hero fotka má byť médium 72 / `jessica-sulev-helpnisi-portrait-stol.png` — naživo sa toto médium používa.
- MCP URL a 401 bez auth — overené.
- Texty sú od klientky, repo je verejné — z README a praxe.
- Menu položky bez odkazov — overené v HTML.
- CTA na `#kontakt` — overené; kotva na stránke chýba — overené.
- Placeholdery fotiek a recenzií — overené.
- MCP pasce (draft vs publish, cache, padding, width, radial-gradient, image JSON, no upload, fade/opacity) — berieme ako prevádzkovú pravdu projektu; parser Elementoru z tejto relácie nebol znovu testovaný zápisom.

## Zastarané

| Tvrdenie | Kde | Realita 2. 10. 2026 |
|---|---|---|
| Hero portrét má malé rozlíšenie, zdroj 440 px | `CLAUDE.md` otvorené veci | Aktuálny hero je médium **72**, **880×1044**. 440×784 je starší súbor médium **47**, na úvodnej stránke sa nepoužíva |
| `get-page-structure` a MCP zápis ako bežná cesta v cloude | implicitne | Bez `HELPNISI_MCP_AUTH` cloud agent MCP nevidí |
| „Obsah každej sekcie má class `xxx-section`“ ako fakt o DOM | `CLAUDE.md` dizajn | Vo verejnom HTML tieto classy nie sú; V4 dáva hash classy. Ostáva to **stavebná dohoda** pre nové sekcie, nie popis dnešného DOM |

## Duplicitné

- `AGENTS.md` opakuje 4 vety z `CLAUDE.md` / README. Zámerne krátke; po tomto audite ukazuje sem, nie kopíruje dizajn.
- README aj `CLAUDE.md` opisujú MCP auth. README ostáva návod na pripojenie. Pravidlá vývoja sú tu.

## Konfliktné

1. **Rozlíšenie hero fotky** — pozri zastarané. Staré tvrdenie nenechávaj ako fakt.
2. **WooCommerce** — pôvodné docs ho nespomínajú. Na webe je eshop, produkt, Besteron. Buď je to mimo aktuálneho sústredenia, alebo docs boli úzke. AI to nesmie ignorovať, keď požiadavka ide do obchodu, ani to nesmie samé „dobudovať“.
3. **Tón produktu Afirmačné kartičky** vs. tón úvodnej stránky. Dva texty, jeden brand. Ktorý je záväzný pre eshop: **neznáme**.
4. Site title `Template` vs. značka helpnisi.

Pri konflikte dokumentácie a živej stránky platí živá stránka ako technická pravda. Pri konflikte dvoch produktových tónov sa AI spýta, neprepisuje.

## Chýbajúce (AI by to potrebovala a projekt to jasne nepíše)

- Kam majú viesť O mne, Metódy, Pre koho, Blog, Kontakt, VOP, GDPR, „Viac o metóde“, Support CTA
- Či je eshop v MVP
- Kam chodí e-mail z formulára
- Manuály na webové texty — Matúš ich mal vložiť (mimo tento repo ako `nastroje/web/texty.md`). Z nich sa má zložiť jeden postup, nie vymyslieť všeobecný copy playbook
- Produkčná doména, termín spustenia, SEO
- Systematický zápis mobilného správania (dnes vieme len: menu `display:none` pod 767 px)
- Alt texty
- Oficiálny zoznam „toto je MVP / toto nie je“
- Testy a spôsob purge cache inak ako ručne v adminovi (MCP nástroj na cache v tejto relácii nebol k dispozícii)

## Čo bolo v pôvodnej dokumentácii dobré

`CLAUDE.md` je hustý a praktický: ID dokumentov, paleta, 1140, MCP pasce, zákaz meniť texty klientky, zákaz hesla v gite. Bez toho by sa web cez AI rýchlo rozpadol. Táto knowledge base to nerozbíja — rozširuje to o produkt, mapu obsahu, oddelenie plánu od implementácie a o overený stav webu.
