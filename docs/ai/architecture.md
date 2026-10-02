# Architektúra

Overené 2. októbra 2026. V tomto projekte **nie je** aplikačný kód v `src/`. „Kód“ je predovšetkým strom Elementoru vo WordPresse plus pár konfiguračných súborov v gite.

## Technológie (z živej stránky)

| Vrstva | Čo beží | Ako overené |
|---|---|---|
| CMS | WordPress 7.1.2 | meta generator |
| Téma | Hello Elementor 3.5.1 | CSS cesty, `theme-hello-elementor` |
| Page builder | Elementor 4.3.3, editor V4 / atomic prvky | meta generator, HTML `e-atomic-element` |
| Theme Builder | Elementor Pro (header 79, footer 80) | CSS `local-79`, `local-80`, `CLAUDE.md` |
| E-shop | WooCommerce 11.1.2 | meta generator, REST `wc/store` |
| Platby | plugin Besteron 2.1.3 | CSS pluginu v HTML |
| Formulár | Elementor Form (nie CF7 / WPForms) | HTML `data-element_type="e-form"` |
| Hosting | HTTPS, nginx, HSTS | HTTP hlavičky |
| Časové pásmo | Europe/Bratislava | WP REST |

AI/Cursor pravidlá v gite: `CLAUDE.md`, `AGENTS.md`, `.mcp.json`, `.cursor/mcp.json`. Táto zložka `docs/ai/` ich dopĺňa a je zdroj pravdy pre budúci vývoj.

## Čo je v gite a čo nie

```
repo (git)
├── docs/ai/          knowledge base a workflow
├── .cursor/          MCP pre Cursor, rules, commands
├── .mcp.json         MCP pre Claude Code
├── images/           podklady; nie všetky sú použité na živej stránke
├── CLAUDE.md         krátky vstup + MCP pasce
├── AGENTS.md         vstup pre Cursor
└── README.md         ako sa pripojiť

WordPress (nie v gite)
├── stránky, šablóny, CSS Elementoru
├── médiá
├── WooCommerce produkty a objednávky
└── formuláre a ich notifikácie
```

Obsah webu sa **necommituje** ako HTML. Meniť sa má cez MCP `template-elementor`, potom publikovať, potom vyčistiť cache.

## Vrstvy

```
prehliadač
    ↓
Hello Elementor (kostra) + Elementor CSS (dizajn a layout)
    ↓
Theme Builder: Header 79 (sticky) + Footer 80
    ↓
Stránka 19 „Domov“ — atomic flexboxy a widgety
    ↓
WordPress + (voliteľne) WooCommerce
```

- **UI** je v Elementore (V4 atomic: `e-flexbox`, `e-div-block`, widgety, `e-form`).
- **Business logika webu** takmer nie je v kóde. Pravidlá sú textové (tón, cena na stránke, „nemente texty klientky“) a v správaní formulára / WooCommerce.
- **Dáta** sú v WordPresse: dokumenty, médiá, produkt ID 16, obsah formulárov.
- **Testy** v repozitári **nie sú**. Overenie = živá stránka, HTML, prípadne MCP `get-page-structure`.

## Entry pointy

| Vstup | ID / cesta | Poznámka |
|---|---|---|
| Domov | WP stránka 19, slug `domov`, šablóna `elementor_header_footer` | hlavná práca |
| Header | Elementor Theme Builder 79 | custom CSS: `position: sticky` |
| Footer | Elementor Theme Builder 80 | |
| MCP | `https://helpnisi.matusbabiak.sk/wp-json/elementor/mcp/` | HTTP Basic, env `HELPNISI_MCP_AUTH` |
| Verejné REST | `/wp-json/wp/v2/…`, `/wp-json/wc/store/v1/…` | čítanie bez hesla, nie zápis |

Názov webu vo WordPresse je stále **Template**. Title úvodnej stránky je `Template`. To nie je produktový názov, len nenastavený site title.

## Ako spolu časti komunikujú

1. Človek (alebo AI) navrhne zmenu.
2. Planning Agent overí knowledge base + živý web / MCP.
3. Po schválení Implementation Agent volá MCP nástroje Elementoru.
4. MCP ukladá **koncept (draft)**. Kým sa nezavolá `publish-document`, živá stránka sa nezmení.
5. `get-page-structure` číta **publikovanú** verziu, nie koncept — preto sa publikuje po každom kroku.
6. Po publikovaní treba vyčistiť cache Elementoru (Nástroje → Clear Files & Data). Inak prehliadač ukáže staré CSS.
7. Repozitár sa aktualizuje len keď sa zmení pravidlo, ID, podklad alebo táto dokumentácia.

Bez `HELPNISI_MCP_AUTH` AI web **nevie** upravovať. Server MCP na neprihlásený request vracia 401.

## Spustenie a deploy

Toto nie je `npm start` projekt.

- Lokálne: naklonovať repo, nastaviť `HELPNISI_MCP_AUTH`, otvoriť v Cursore.
- „Deploy“ stránky = publikovanie dokumentu v Elementore + purge cache.
- GitHub slúži na zdieľanie kontextu medzi zariadeniami, nie na build frontendu.
- CI/CD v repozitári **nie je**.

Cloudový agent potrebuje v prostredí premennú `HELPNISI_MCP_AUTH` a povolenú doménu `helpnisi.matusbabiak.sk`.

## Mapovanie: obrazovka → prvky → pravidlá → dáta → testy

| Obrazovka | Z čoho je zložená | Pravidlá | Dáta | Testy |
|---|---|---|---|---|
| Domov | Elementor atomic na stránke 19 + header 79 + footer 80 | dizajn 1140 px, texty klientky, CTA na formulár | médiá, texty v Elementore, formulár | žiadne automatické; vizuál + HTML |
| Hlavička | logo (médium 87), 5 textov menu, CTA tlačidlo | sticky, blur, menu zatiaľ bez URL | médium 87 | na mobile je menu `display:none` (overené v CSS) |
| Formulár | Elementor Form, polia meno/priezvisko/email/správa | povinné polia, slovenské hlášky | kam ide mail: neznáme | odoslanie naživo; v tejto relácii neodosielané |
| Obchod | WooCommerce šablóny, nie Elementor landing | **neznáme**, či je v MVP | produkt ID 16, 42,99 € | žiadne v gite |
| Blog | predvolený článok | **neznáme** | post ID 1 „Ahoj svet!“ | — |

## CSS a class names

V dokumentácii je dohoda: vonkajší obal sekcie `xxx-section`, vnútorný kontajner `max-width: 1140px`.

Vo **verejnom HTML** sa sémantické classy typu `hero-section` **nenachádzajú**. Elementor V4 generuje hash classy (`e-370f69f2-8dec`). Dohoda `xxx-section` je **stavebné pravidlo pre nové sekcie**, nie overený názov v DOM.

Farby, 1140 px, Inter, DM Serif Display, `border-radius: 9999px` **sú** v publikovanom CSS stránky 19, headeru 79 a footera 80.

## MCP pasce (stále platné)

Podrobne v `CLAUDE.md`. Zhrnutie, overené praxou projektu:

1. Po `manage-elements` / `build-composition` / `update-page-settings` vždy `publish-document`.
2. Publikovať aj medzi krokmi, inak ďalší nástroj číta starý strom.
3. Po publikovaní Clear Files & Data.
4. `get-page-structure` = publikované, nie draft.
5. Nemiešať `max()` / `calc()` s bežným paddingom v jednom `padding`.
6. Absolútne prvky: nastav `width` ručne.
7. `radial-gradient` parser neberie; `linear-gradient` áno.
8. Obrázok: `{"image": {"src": {"id": <ID>, "alt": "…"}, "size": "full"}}`.
9. MCP nenahráva súbory do Médií.
10. Animácia `fade` vie prepísať `opacity`.

Tieto pasce Implementation Agent dodržiava vždy. Planning Agent ich berie do úvahy pri návrhu (nerobí plán, ktorý MCP nevie bezpečne vykonať).
