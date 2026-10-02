# Business rules

Pravidlá, ktoré AI pri ďalšom vývoji nesmie porušiť. Zdroj: živý web, `CLAUDE.md`, tento repozitár. Čo nie je overené, nie je pravidlo.

Stupne:

- **Kritické** — porušenie vie zverejniť tajomstvo, zničiť obsah, ublížiť dôvere klientky alebo právne ohroziť.
- **Dôležité** — porušenie pokazí produkt alebo dizajn, ale dá sa vrátiť.
- **Bežné** — konvencie, ktoré držia prácu konzistentnú.

## Kritické

1. **Žiadne tajomstvá v gite.** Repozitár je verejný. Nikdy nezapisuj `HELPNISI_MCP_AUTH`, heslá, Application Passwords, `.env` s vyplnenou hodnotou, base64 prihlasovací reťazec.
2. **Texty na webe sú od klientky.** Nemeň ich, neprepisuj, neskrať a nevylepšuj bez výslovného pokynu. To platí aj pre „drobné“ štylistické úpravy.
3. **Nevymýšľaj recenzie ani sľuby výsledku.** Placeholdery výslovne zakazujú sľubovať vyliečenie. Ostrý text recenzie sa smie vložiť len keď ho dodá Matúš / klientka.
4. **Nemaž a neprepisuj celé šablóny** (stránka 19, header 79, footer 80) ako „refactor“. Žiadne prázdne `build-composition` namiesto malej opravy.
5. **Nesahej na WooCommerce objednávky, platobnú bránu, produkčné URL, indexáciu** (`noindex`) a site title bez pokynu. Toto je vývojová adresa.
6. **Neodstraňuj existujúcu funkciu**, ktorú požiadavka nespomína (formulár, sticky header, CTA, obsah sekcií).
7. **MCP: draft nie je live.** Zmena bez `publish-document` nie je hotová. Zmena bez vyčistenia cache môže naživo vyzerať, že „sa nič nestalo“, a ďalší krok potom rozbije strom.

## Dôležité

8. **Najmenšia správna zmena.** Ak stačí pridať `id="kontakt"`, nestránaj celú Contact sekciu.
9. **Existujúci pattern pred novou architektúrou.** Nové sekcie: vonkajší obal + vnútorný 1140 px kontajner. Nové tlačidlá: pilulka. Farby z palety. Žiadny nový builder, žiadny custom plugin „lebo by to bolo čistejšie“.
10. **Šírka obsahu 1140 px.** Padding vonkajšej sekcie nerieš cez `max()`/`calc()` zmiešané s bežnými hodnotami.
11. **Dve vrstvy sekcie.** Vonkajšok nesie pozadie a odsadenie (desktop `4.5rem 3rem`, mobil `3rem 1.25rem`). Vnútro: `width: 100%; max-width: 1140px; padding: 0`, centrované.
12. **Nepridávaj odkazy na neexistujúce stránky**, kým nie je jasné kam majú viesť. Vymyslená URL je horšia ako text bez odkazu.
13. **Formulár ostáva povinný v aktuálnych poliach**, kým to niekto nezmení zámerne. Neodstraňuj `required`, nepridávaj polia „pre istotu“.
14. **Ceny.** Na úvodnej stránke je konzultácia 45 €. V obchode kartičky 42,99 €. Nemeň sumy a nespájaj ich.
15. **Tón.** Integratívna terapia, nie rýchly fix. Oslovenie na stránke je väčšinou ženské. Nemeň rod ani sľub horizontu 1–1,5 roka.
16. **Obrázky.** MCP nenahráva médiá. Použi existujúce ID z knižnice. Nevymýšľaj ID. Alt text sa má vyplniť, keď sa obrázok nastavuje — vo WP sú dnes prázdne.
17. **Animácie.** Len veľmi jemné. Žiadne pomalé posuny blokov s textom (sekajú). `fade` nedávaj na prvky so zníženou opacity.

## Bežné

18. Po každej úprave webu: MCP zmena → publish → cache → kontrola živej stránky.
19. Ak sa zmení ID dokumentu, médium, nové pravidlo alebo nová sekcia, aktualizuj túto knowledge base v tom istom kole.
20. Title webu je zatiaľ `Template`. Nemeň ho „po ceste“, ak to nie je zadanie.
21. Menu na mobile je schované CSS-om. Úprava menu musí počítať s týmto stavom, nie predpokladať desktop.
22. V jednom kole sa rieši **hlavná priorita** — jedna vec, zvyšok čaká.
23. Copy playbook sa nemá vymýšľať. Keď príde práca na textoch, najprv použiť Matúšove manuály (ešte nie sú v tomto repozitári).

## Validácie a stavy, ktoré existujú

| Miesto | Pravidlo |
|---|---|
| Formulár | 4 povinné polia, e-mail type, success/error hlášky po slovensky |
| CTA | viacero tlačidiel mieri na `#kontakt`, kotva musí ostať v súlade s href |
| Header hover | položky menu a zelené tlačidlo menia farbu na terakotu |
| WooCommerce | produkt 16 je simple, in stock, 42,99 EUR — nemeň typ produktu bez zadania |

Stavové automaty objednávok, login, role — v tomto repozitári **nie sú zdokumentované** a AI ich nemá meniť.

## Bezpečnosť

- MCP endpoint vracia 401 bez Basic auth. To je správne; neobchádzaj to.
- Verejné REST čítanie stránok a médií je v poriadku na audit. Zápis len cez MCP po schválení.
- Nespúšťaj WP-CLI, SQL, reset databázy, zmenu používateľov.
