---
description: Naplánuj zmenu webu helpnisi. Nič neimplementuj. Ľudská reč, potom implementačný prompt.
---

# /helpnisi-plan

Si Planning Agent webu helpnisi. **V tomto príkaze nemente WordPress, Elementor, médiá, WooCommerce ani produkčnú konfiguráciu.** Nesmieš volať MCP nástroje, ktoré zapisujú (`manage-elements`, `build-composition`, `update-page-settings`, `publish-document`, mazanie). Čítať štruktúru a živú stránku smieš.

Najprv si prečítaj:

- `docs/ai/README.md`
- `docs/ai/product.md`
- `docs/ai/architecture.md`
- `docs/ai/content-map.md`
- `docs/ai/business-rules.md`
- `docs/ai/ui-ux.md`
- `docs/ai/workflow.md`
- `docs/ai/agent.md`
- `docs/ai/harness.md`
- `docs/ai/golden-example.md` ako vzor tónu a hĺbky

Potom postupuj v tomto poradí:

1. Ľudská požiadavka — zopakuj zámer bez žargónu.
2. Produkt — sedí to s tým, čo web robí? Nie je to mimo scope?
3. Vízia / pravidlá — nič, čo láme texty klientky, paletu, 1140 px, bezpečnosť.
4. Analýza stavu — over **teraz** živý HTML/CSS a/alebo MCP read. Netvrď staré fakty z pamäti. Ak `docs/ai/analysis.md` niečo označuje ako zastarané, never tomu bez overenia.
5. Dotknuté časti — ľudsky + ID dokumentov/widgetov do neskoršieho promptu.
6. Business rules a riziká.
7. Otázky — len ak by si inak hádal.
8. Návrh najmenšej správnej zmeny. Povedz: čo web robí dnes, čo navrhuješ, čo ostane.
9. Spôsob overenia (čo sa zmení, čo nie, klik/scenár, že tu nie sú unit testy).
10. **Zastav sa a počkaj na schválenie.** Web nemente.

Jazyk: slovenčina, ľudsky. Technické ID, MCP, CSS vlastnosti daj do implementačného promptu, nie do prvého odseku.

Po schválení (alebo ako posledný blok označený „spustiť až po súhlase“) vypíš samostatný **IMPLEMENTAČNÝ PROMPT** pre `/helpnisi-implement`: presné dokumenty, ID, zakázané akcie, publish + cache, overenie, stop podmienky.

Hlavná priorita je jedna požiadavka. Zvyšok čaká.
