# Mapa obsahu

Toto je namiesto dátového modelu. Dáta webu sú dokumenty WordPressu, médiá, texty v Elementore, jeden formulár a jeden WooCommerce produkt.

Overené 2. októbra 2026. ID dokumentov 19 / 79 / 80 sú z `CLAUDE.md` a sedia s publikovaným CSS (`local-19`, `local-79`, `local-80`) a REST stránkou 19.

## WordPress dokumenty

| ID | Typ | Názov | URL / podmienka |
|---|---|---|---|
| 19 | stránka | Domov | `/`, šablóna `elementor_header_footer` |
| 79 | Theme Builder | Helpnisi – Header | `include/general` (podľa `CLAUDE.md`) |
| 80 | Theme Builder | Helpnisi – Footer | `include/general` (podľa `CLAUDE.md`) |
| 13 | stránka | Môj účet | `/moj-ucet/` |
| 12 | stránka | Pokladňa | `/kontrola-objednavky/` |
| 11 | stránka | Košík | `/kosik/` |
| 10 | stránka | Obchod | `/obchod/` |
| 16 | produkt | Afirmačné kartičky | `/produkt/afirmacne-karticky/` |
| 1 | príspevok | Ahoj svet! | `/ahoj-svet/` |

Elementor knižnica (header/footer ako `elementor_library`) nie je verejne čitateľná (REST 401).

## Domov — sekcie v poradí

Poradie podľa `CLAUDE.md` a podľa nadpisov na živej stránke. Sémantické HTML `id` má len kontaktná sekcia (`id="kontakt"` na vonkajšom obale `56037d37`). Ostatné sekcie `id` nemajú.

| # | Interný názov | Čo tam je naživo | Medzery |
|---|---|---|---|
| 1 | Hero | Štítok Psycho/Bio/Socio/Spirituálno, H1, odseky, CTA, portrét ID 72, kartička mena | — |
| 2 | Problems | „Možno navonok fungujete…“ + zoznam tém | — |
| 3 | Main Idea | Minulosť vs. dnešok, „Pozerám sa na človeka ako na celok.“ | — |
| 4 | Whole | Psycho / Bio / Socio / Spirituálno | text „Foto – nahrať do Media Library“ |
| 5 | Approach | Prepojenie smerov, zoznam metód | — |
| 6 | Methods | 6 kariet metód, „Viac o metóde →“ **nie je odkaz** | podstránky metód neexistujú |
| 7 | Expertise | Odbornosť a spiritualita, citát, foto placeholder | „Foto Jessicy – nahrať do Media Library“ |
| 8 | Start | 3 kroky k konzultácii | CTA idú na `#kontakt` |
| 9 | Trust | Vzdelanie, výcviky, 5 rokov; 3× „Foto klientky“ | fotky aj recenzie v Trust nie sú hotové |
| 10 | Contact | Formulár „Homepage konzultácia“ | `id="kontakt"` na vonkajšom obale `56037d37`, `scroll-margin-top: 7rem` |
| 11 | Support | 3 ponuky podpory | 3× „Foto – nahrať“, CTA nie sú odkazy |
| 12 | Reviews | 4 karty s placeholderom recenzie | vymyslený text recenzie sa nesmie použiť ako ostrý |

Hlavička a pätička sedia nad / pod týmto obsahom na každej stránke s Theme Builder podmienkou general.

## Hlavička (79)

Viditeľné texty: logo, **O mne**, **Metódy**, **Pre koho**, **Blog**, **Kontakt**, tlačidlo **Dohodnúť konzultáciu**.

Overené v HTML:

- logo odkazuje na `https://helpnisi.matusbabiak.sk`
- CTA odkazuje na `/#kontakt` (cieľ existuje na stránke 19)
- päť položiek menu **nemá** `<a href>`
- v CSS je `backdrop-filter: blur(14px)`, tieň ako v `CLAUDE.md`, sticky cez custom CSS šablóny 79
- na **mobile** (`max-width: 767px`) je kontajner menu `display:none` — položky menu na úzkom displeji nie sú vidno

## Pätička (80)

Stĺpce: citát / Služby / Kontakt / Dokumenty.

- Telefón `0951 015 423` → `tel:+421951015423` (funguje)
- E-mail `info@helpnisi.sk` → `mailto:` (funguje)
- Adresa: Koceľova 17, 821 08 Bratislava
- Hodiny: PO–PIA 10:00–20:00, SO–NE zatvorené
- Položky Služieb, VOP a Ochrana osobných údajov **nie sú odkazy**
- Pozadie `#FCD9CE`, vnútorná šírka 1140 px

## Formulár

- Živý widget: V4 atomic `e-form` (`data-id="4d469f35"`), **nie** klasický Elementor Pro Form (`widgetType=form` / `.elementor-form`)
- Názov: Homepage konzultácia
- Polia: `contact-first-name`, `contact-last-name`, `contact-email`, `contact-message` — všetky `required`, placeholdery Meno / Priezvisko / Email / Vaša správa
- Submit: „Dohodnúť si konzultáciu“ (`type=submit`)
- Úspech: „Ďakujem. Ozvem sa vám čoskoro.“
- Chyba: „Správu sa nepodarilo odoslať. Skúste to prosím znova.“
- Kotva `#kontakt`: **existuje** na vonkajšom obale sekcie `56037d37` (H2 + formulár). Nie na inpute.
- CTA s `href` `#kontakt` alebo `/#kontakt` (nemenili sa): header `167100bb` (`/#kontakt`), homepage `78d5a485`, `61254e9f`, `25dbcc77`, `2b64532c`, `4f40c68f`
- E-mailová akcia: v tomto kole sa **nenastavovala**. Na existujúcom atomic `e-form` je v editore už vyplnená (nemazalo sa). Klasický Pro Form sa cez MCP **nepodarilo vložiť** — `elementor-list-widget-schemas` typ `form` neponúka, `get-widget-schema` pre `form` vracia „Unknown widget type“, `build-composition` s `<form>` vytvorí 0 prvkov. Editor cez MCP ponúka atomic `e-form` + `e-form-input` / `e-form-textarea` / `e-form-submit-button`. Atomic form ani HTML fake sa namiesto Pro Form nedávali.

## Médiá

Súbory v `images/` a vo WP Media Library (verejné REST). Alt texty sú vo WP **prázdne**.

| WP ID | Súbor | px | Na živej úvodnej stránke |
|---|---|---|---|
| 87 | `helpnisi-logo.png` | 144×63 | áno, header aj footer |
| 72 | `jessica-sulev-helpnisi-portrait-stol.png` | 880×1044 | áno, hero |
| 69 | `jessica-sulev-helpnisi-portrait.png` | 880×956 | v knižnici, na úvodnej nie |
| 57 | `jessica-sulev-helpnisi-cutout.png` | 880×1016 | v knižnici, na úvodnej nie |
| 47 | `jessica-sulev-helpnisi.jpg` | **440×784** | starší portrét, na úvodnej **nie** (hero používa 72) |
| 58 | `afirmacne-karticky.jpg` | 330×330 | v knižnici; Support sekcia má placeholder |
| 59 | `individualna-terapia.jpg` | 330×330 | v knižnici; Support placeholder |
| 60 | `programy-a-meditacie.jpg` | 330×330 | v knižnici; Support placeholder |
| 62–64 | `video-referencia-1.jpg` … `3.jpg` | ~240×428 | v knižnici; recenzie sú textové placeholdery |
| 36 | `helpnisi-hero-therapy-room.png` | 1596×2399 | v knižnici, **nie v gite** |
| 9 | WooCommerce placeholder | 1200×1200 | systémový |

`CLAUDE.md` píše, že hero má malé rozlíšenie „zdroj 440 px“. To sedí na médium **47**, nie na aktuálny hero **72** (880 px). Pozri [analysis.md](./analysis.md).

## WooCommerce

- Mena: EUR
- Produkt 16: Afirmačné kartičky, **42,99 €**, simple, purchasable, in stock, bez obrázka v Store API
- Popis produktu je predajnejší než tón úvodnej stránky. Či ho schválila klientka: **neznáme**
- Na úvodnej stránke je konzultácia **45 €** — iná suma, iná služba

## Čo sa na webe tvári ako odkaz, ale nie je

Overené prechodom všetkých `<a>` na úvodnej stránke. Funkčné odkazy sú len: skip link, logo, CTA na `#kontakt`, tel, mailto.

Nie sú odkazy: menu, položky pätičky okrem tel/mail, „Viac o metóde →“, „Chcem lepšie porozumieť sebe →“, „Chcem pracovať vlastným tempom →“, „Chcem podporu na každý deň →“, VOP, GDPR.

## Title a indexácia

- Site name aj `<title>` úvodnej stránky: `Template`
- `robots`: `noindex, nofollow`

To je vývojový web, nie ostrá indexácia.
