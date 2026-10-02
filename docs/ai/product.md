# Produkt: helpnisi

Overené 2. októbra 2026 z živej stránky https://helpnisi.matusbabiak.sk, verejného WordPress REST API a súborov v tomto repozitári. Čo nie je overené, je označené ako **neznáme**.

## Čo web robí

helpnisi je web terapeutky **Mgr. Jessicy Sulev**. Predstavuje integratívnu terapiu: odborné prístupy, práca s telom, minulosťou, emóciami a spiritualitou podľa konkrétneho človeka.

Hlavný sľub na úvodnej stránke:

> Terapia, ktorá sa nepozerá iba na problém. Ale na celého človeka.

Značka pracuje s rámcom **Psycho • Bio • Socio • Spirituálno**.

## Pre koho

Z úvodnej stránky vyplýva, že hovorí predovšetkým k **ženám** (oslovovanie „vyčerpaná“, „zažila“, „mohla“, „sama“). Témy, ktoré stránka menuje:

- úzkosť a vnútorné napätie
- smútok a životné krízy
- psychosomatické ťažkosti
- vyhorenie a workoholizmus
- perfekcionizmus
- sebavedomie a sebahodnota
- vzťahy a opakujúce sa vzorce
- hľadanie smeru
- napojenie na seba

Presný marketingový segment (vek, mesto, kanály) **nie je v projekte definovaný**.

## Aký problém rieši

Stránka hovorí, že ťažkosti nemusia byť izolovaný problém, ale súčasť širšieho príbehu. Nesľubuje rýchle vyliečenie. Naopak, pri pravidelnej dlhodobej práci spomína horizont **jedného až jeden a pol roka**.

## Hlavný používateľský cieľ

Z CTA na stránke: **dohodnúť si vstupnú konzultáciu** cez formulár. Cena na stránke: **Vstupná konzultácia: 45 €**.

Ďalšie ponuky v sekcii podpory (zatiaľ bez funkčných odkazov na webe):

- individuálna práca s Jessicou
- vedené programy a meditácie
- 50 afirmačných kartičiek s manuálom

## Hlavné flows

### Flow A — záujem o konzultáciu (hlavný)

1. Človek príde na úvodnú stránku.
2. Číta, s čím helpnisi pracuje.
3. Klikne na tlačidlo typu „Dohodnúť konzultáciu“ / „Chcem začať“.
4. **Zámer:** dostať sa na formulár.
5. **Aktuálny stav:** tlačidlá idú na `#kontakt`, ale na stránke **nie je** `id="kontakt"`. Formulár existuje, kotva nie.
6. Formulár žiada: Meno, Priezvisko, Email, správa (všetko povinné).
7. Po odoslaní má ukázať: „Ďakujem. Ozvem sa vám čoskoro.“ alebo chybu.

Kam e-mail z formulára reálne ide: **neznáme** (nie je vo verejnom HTML).

### Flow B — zorientovať sa v prístupe

Človek prechádza sekcie: problém → celok človeka → Psycho/Bio/Socio/Spirituálno → metódy → odborný profil → kroky → dôvera → formulár → ďalšia podpora → recenzie.

### Flow C — kúpiť kartičky (existuje v WooCommerce, na úvodnej stránke nie je napojené)

V obchode je produkt **Afirmačné kartičky**, 42,99 €, skladom, platobná brána Besteron je nainštalovaná. Karty na úvodnej stránke („Chcem podporu na každý deň“) **nie sú odkazy**. Či je nákup súčasťou aktuálneho MVP, je **neznáme**.

### Flow D — blog / podstránky z menu

V hlavičke sú texty O mne, Metódy, Pre koho, Blog, Kontakt. **Nie sú to odkazy.** Jediný článok je predvolený WordPress „Ahoj svet!“. Kam majú položky menu viesť: **neznáme**.

## Hlavné obrazovky (overené)

| Obrazovka | URL | Stav |
|---|---|---|
| Domov | `/` (stránka ID 19) | Hlavný obsah, Elementor |
| Obchod | `/obchod/` | WooCommerce, predvolená šablóna, 1 produkt |
| Produkt | `/produkt/afirmacne-karticky/` | Afirmačné kartičky |
| Košík / pokladňa / účet | `/kosik/`, `/kontrola-objednavky/`, `/moj-ucet/` | Predvolené WooCommerce stránky |
| Článok | `/ahoj-svet/` | Predvolený Hello World |

Ďalšie marketingové podstránky (O mne, metódy, VOP, GDPR) vo verejnom zozname stránok **nie sú**.

## Hlavné funkcie, ktoré web dnes reálne má

- úvodná stránka s 12 sekciami (pozri [content-map.md](./content-map.md))
- sticky hlavička s logom, textovým menu a zeleným CTA
- pätička s kontaktom (telefón a e-mail **sú** odkazy)
- Elementor formulár „Homepage konzultácia“
- WooCommerce + 1 produkt + Besteron plugin
- `noindex, nofollow` — ide o vývojovú adresu, nie o verejný SEO web

## Produktové rozhodnutia, ktoré už sú v projekte

Tieto veci sú v pravidlách alebo na webe dosť jasné na to, aby ich AI nemenila bez pokynu:

- značka sa volá **helpnisi** (malé h), osoba je Mgr. Jessica Sulev
- web stavia Matúš; obsah textov je od klientky
- vývojová adresa je subdoména `helpnisi.matusbabiak.sk`
- vizuál: tmavozelená + terakota + broskyňové tóny, DM Serif Display + Inter, šírka obsahu 1140 px
- terapia je integratívna, nie „vyberte si metódu z cenníka“
- recenzie nesmú sľubovať vyliečenie (aj placeholdery to pripomínajú)
- texty na webe sa nemente bez pokynu

## Čo vyzerá ako aktuálne MVP

Z toho, čo je postavené a na čom sa pracuje:

- jedna silná úvodná stránka
- cesta k vstupnej konzultácii
- dôvera (vzdelanie, výcviky, 5 rokov helpnisi)
- vizuál a tón

Nie je povedané nahlas v dokumentácii, že toto **je** oficiálne MVP. Je to odvodenie zo stavu webu. Označuj to opatrne.

## Čo je mimo scope, kým to Matúš výslovne neotvorí

- prepisovanie textov klientky
- vymýšľanie recenzií
- SEO a indexácia (stránka je `noindex`)
- produkčná doména — **neznáma**
- systematický redesign
- nové podstránky bez zadania kam majú viesť
- zmena ceny konzultácie alebo obchodu bez pokynu

## Neznáme (nevymýšľať)

- kam majú viesť položky menu a pätičky
- či existujú (alebo majú vzniknúť) stránky metód, VOP, GDPR
- či je WooCommerce súčasťou spustenia, alebo zatiaľ len nainštalovaný
- či text produktu Afirmačné kartičky schválila klientka (tón je iný ako na úvodnej stránke)
- kam chodí e-mail z formulára
- otváracie hodiny: na webe sú PO–PIA 10:00–20:00, SO–NE zatvorené — či sedia s realitou, neoverené mimo webu
- adresa Koceľova 17, Bratislava — na webe je, fyzickú prevádzku AI neoverovala
- kedy a ako prejsť z vývojovej adresy na ostrú
- manuály Matúša na webové texty (mali byť v `nastroje/web/texty.md`, v tomto repozitári nie sú)

Keď požiadavka závisí od niektorého z týchto bodov, Planning Agent sa má spýtať, nie si odpoveď vymyslieť.
