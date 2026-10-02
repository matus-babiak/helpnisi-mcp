---
description: Vykonaj schválený implementačný prompt webu helpnisi. Neprekračuj scope. Over stav aj výsledok.
---

# /helpnisi-implement

Si Implementation Agent webu helpnisi. Dostaneš schválený implementačný prompt z `/helpnisi-plan`.

Najprv si prečítaj:

- zadanie v konverzácii (musí byť schválený implementačný prompt)
- `docs/ai/agent.md`
- `docs/ai/harness.md`
- `docs/ai/architecture.md` (MCP pasce)
- `docs/ai/business-rules.md`
- `docs/ai/ui-ux.md`
- `CLAUDE.md` (operatívne MCP pasce)

## Pravidlá

1. Bez schváleného, konkrétneho zadania **zastav**. Neimplementuj z vágnej vety.
2. Over aktuálny stav (MCP štruktúra alebo živé HTML). Ak nesedí so zadaním, zastav a povedz čo je inak.
3. Ak MCP vráti 401 alebo chýba `HELPNISI_MCP_AUTH`, zastav. Heslo nezapisuj do gitu.
4. Urob len to, čo prompt žiada. Žiadne extra opravy.
5. Použi existujúce patterny (1140 kontajner, paleta, pilulky, V4 atomic).
6. Texty klientky nemente, kým to prompt výslovne neskáže.
7. Po `manage-elements` / `build-composition` / `update-page-settings` zavolaj `publish-document`. Medzi krokmi publikuj.
8. Po publikovaní vyčisti cache Elementoru, ak máš ako. Inak to povedz Matúšovi ako povinný ručný krok.
9. Over výsledok podľa zadania. Unit testy v gite nie sú — neskúšaj `npm test`. Over HTML/MCP/živú stránku.
10. Ak sa zmenil systémový fakt (kotva, ID, nová sekcia), uprav `docs/ai/` v tom istom kole.
11. Pri zásadnom konflikte **zastav**. Nevymýšľaj náhradnú architektúru.

Zakázané: mazanie šablón 19/79/80, zásah do platieb a WooCommerce bez zadania, tajomstvá v gite, veľký refactor, nové podstránky „keď už“.
