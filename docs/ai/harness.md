# Harness — čo agent nesmie urobiť „omylom“

Primerané tomuto projektu: nie je tu migračný nástroj ani lokálna databáza, ale dá sa zmazať živý web, zverejniť heslo, alebo prepísať šablónu.

## Zakázané bez výslovného zadania

| Riziko | Čo to tu znamená | Čo namiesto toho |
|---|---|---|
| Zmazanie „databázy“ | Mazanie stránok, produktov, médií, formulárov, používateľov vo WP | Nemazať. Maximálne skryť prvok, ak to zadanie chce |
| Nebezpečná migrácia | Hromadný `build-composition` celej homepage, import/export JSON šablóny naslepo | Malý `manage-elements` na konkrétne ID |
| Produkčná konfigurácia | Site URL, permalinky, `noindex`, WooCommerce platby, Besteron, SMTP, účty | Nemeniť |
| Odstránenie funkcie | Formulár, header, footer, CTA, existujúce sekcie | Mimo scope = nedotýkať sa |
| Security | Zápis tajomstva do gitu, vypnutie auth na MCP, verejný dump `.env` | Len `HELPNISI_MCP_AUTH` v prostredí |
| Veľký refactor | „Zjednotíme classy“, „prestavíme V4 na V3“, nový theme | Nie, ak požiadavku splní existujúci pattern |
| Scope creep | Oprava menu pri zadanej kotve formulára | Jedna hlavná priorita |

## Povinné poistky pri zápise na web

1. Existuje schválený implementačný prompt? Ak nie → stop.
2. Beží MCP auth? Ak 401 → stop, povedať Matúšovi že chýba `HELPNISI_MCP_AUTH`.
3. Zmena je na konkrétnych element ID, nie na „celej stránke“.
4. Po kroku `publish-document`.
5. Po sérii krokov cache Elementoru.
6. Kontrola, že nezmizla iná sekcia (porovnaj nadpisy pred/po).
7. Žiadny commit, ktorý obsahuje `.env` alebo auth header.

## Čo harness zámerne neblokuje

- úpravu textu **po výslovnom pokyne**
- pridanie `id`, CSS, odkazu, obrázka z existujúceho média
- úpravu dokumentácie v `docs/ai/`
- čítanie živej stránky a REST API
- malú úpravu padding / farby v rámci palety, ak je to zadanie

Harness nie je zákaz vyvíjať. Je to zákaz ničiť a rozširovať prácu mimo vety, ktorú človek napísal.

## Keď si agent nie je istý, či je akcia nebezpečná

Zastaviť a spýtať sa. Hádať sa nesmie pri mazaní, pri textoch klientky, pri platbách a pri publikovaní na indexovaný web. Tento web je zatiaľ `noindex` — aj tak sa tvár ako na ostrom obsahu, nie ako na hračke.
