# Golden example — Planning Agent na reálnom stave

Dátum overenia: 2. október 2026. Zdroj: HTML úvodnej stránky https://helpnisi.matusbabiak.sk (nie hypotéza).

Toto je vzor, ako má `/helpnisi-plan` vyzerať. **Tento príklad sa nemá vykonať**, kým ho Matúš neschváli ako skutočnú úlohu. Slúži ako predloha správania, nie ako tichý pokyn na úpravu webu.

---

## Používateľská požiadavka

„Keď kliknem na Dohodnúť konzultáciu, chcem sa dostať na formulár.“

## Pochopenie

Chceš, aby tlačidlo, ktoré sľubuje konzultáciu, naozaj otvorilo tú časť stránky, kde sa píše správa Jessice. Nie novú stránku, nie nový formulár.

## Kontext produktu

Hlavný cieľ úvodnej stránky je dohodnúť vstupnú konzultáciu. Formulár už na stránke je (Meno, Priezvisko, Email, správa). Cesta k nemu je teda existujúci flow, nie nový produkt.

## Kontrola dokumentácie

`CLAUDE.md` aj `content-map.md` hovoria: tlačidlá odkazujú na `/#kontakt`, kotva na sekcii s formulárom chýba.

## Kontrola kódu (živé HTML)

Overené v HTML:

- `href='/#kontakt'` na „Dohodnúť konzultáciu“ v hlavičke
- `href='#kontakt'` na ďalších CTA („Dohodnúť si konzultáciu“, „Chcem si dohodnúť konzultáciu“, „Chcem začať“)
- atribút `id="kontakt"` ani `name="kontakt"` na stránke **nie je**
- formulár existuje: Elementor Form, `data-form-name="Homepage konzultácia"`, widgety polí `contact-first-name` atď.

Tlačidlá už miera správnym smerom. Chýba cieľ.

## Dotknuté časti

- sekcia s formulárom na stránke 19
- všetky existujúce CTA, ktoré už majú `#kontakt` — tie **netreba** prepisovať, ak kotva vznikne

Hlavičkové menu „Kontakt“ (text bez odkazu) táto veta **nespomína**.

## Business rules

- najmenšia zmena
- nemente texty
- nemente polia formulára
- nestránajte Contact sekciu kvôli kotve

## Riziká

- ID dať na príliš vnútorný prvok — skok schová nadpis pod sticky header.
- ID dať na zlý wrapper — po ďalšom `build-composition` môže zmiznúť.
- Na mobile sticky header zakryje začiatok formulára (overiť scroll).

## Otázky

1. Má aj nápis **Kontakt** v hornom menu ísť na ten istý formulár, alebo v tomto kole len tlačidlá, ktoré už `#kontakt` majú?
2. Stačí skok na sekciu, alebo chceš aj malý odsadenie pod lepkavou hlavičkou, aby sa nadpis neschoval?

Ak neodpovieš, agent **nesmie** sám pridať odkazy do menu.

## Návrh (ľudskou rečou)

Dnes tlačidlá hovoria prehliadaču „skoč na kontakt“, ale žiadna časť stránky sa tak nevolá. Formulár tam pritom je, len nemá meno.

Navrhujem pomenovať obal sekcie s formulárom ako `kontakt` a nič iné na tej sekcii neriešiť. Texty, polia, farby a ostatné časti stránky ostanú.

## Čo sa nemá meniť

- znenie tlačidiel
- polia a hlášky formulára
- iné sekcie
- menu položky (kým neodpovieš na otázku 1)
- WooCommerce, pätička, fotky

## Ako overíme

1. Na `/` kliknúť „Dohodnúť konzultáciu“ v hlavičke — v okne je formulár, URL končí `#kontakt`.
2. To isté na CTA v spodnej časti stránky.
3. Overiť v HTML, že existuje práve jeden `id="kontakt"`.
4. Hero, menu texty a pätička vyzerajú ako predtým.
5. Desktop aj úzke okno (sticky header nesmie úplne zakryť nadpis, ak sme riešili otázku 2).

Automatické testy v gite nie sú.

## Rozhodnutie (vzor)

Až keď Matúš napíše napríklad: „Áno. Menu zatiaľ nerieš. Odsadenie pod hlavičkou áno, ak treba.“

Bez tejto vety sa web nemení.

## Implementačný prompt (vzor po schválení)

```
Úloha: na publikovanej úvodnej stránke helpnisi (WP ID 19) pridaj kotvu kontakt
k existujúcej sekcii s formulárom. Nič iné.

Overenie pred zmenou:
- MCP get-page-structure na dokument 19, alebo živé HTML.
- Nájdi Elementor Form „Homepage konzultácia“ / polia contact-first-name.
- Nájdi najbližší vonkajší obal tej sekcie (nie samotný input).
- Ak už id=kontakt existuje, zastav a nahlás to. Neduplikuj.

Zmena:
- Nastav HTML id="kontakt" na vonkajší obal sekcie formulára (alebo ekvivalent
  v Elementor V4: css id / attributes na tom containeri).
- Ak sticky header (dokument 79) prekrýva cieľ, pridaj na ten istý obal
  scroll-margin-top primeraný výške headeru. Nerob novú prázdnu medzeru v layoute.
- Nemente texty, polia, tlačidlá, href-y ktoré už sú #kontakt alebo /#kontakt.
- Nemente menu, footer, iné sekcie, WooCommerce.

MCP:
- manage-elements (alebo ekvivalent) len na tento prvok.
- publish-document 19.
- Ak header CSS netreba, dokument 79 nepublikuj.
- Clear Files & Data.
- Medzikroky publikuj, ať get-page-structure neprepisuje draft.

Hotovo keď:
- živé HTML obsahuje id="kontakt"
- klik na Dohodnúť konzultáciu scrolluje na formulár
- na stránke ostáva jeden formulár s tými istými 4 poľami
- H1 hero je nezmenené

Zakázané: nové stránky, nové formuláre, zmena copy, úprava recenzií,
vymyslené URL, zápis tajomstiev, refactor celej homepage.

Ak MCP vráti 401 alebo strom nesedí so zadaním, zastav.
```

Tento prompt je pripravený na `/helpnisi-implement`. Planning Agent ho v ostrom kole vygeneruje až po schválení a upraví podľa odpovedí na otázky.
