# Workflow: plánovanie oddelené od implementácie

Toto je jediný podporovaný spôsob, ako má AI meniť web helpnisi.

## Hlavná priorita

V jednom kole sa rieši **jedna** požiadavka. Zvyšok čaká. Neskladaj „ešte aj menu, ešte aj fotky, ešte aj title“ do jedného plánu, ak to človek nechcel.

## Tok

```
ľudská veta
    → /helpnisi-plan
    → pochopenie + produkt + dokumentácia + živý web
    → riziká a otázky
    → návrh ľudskou rečou
    → tvoje schválenie (a odpovede)
    → implementačný prompt
    → /helpnisi-implement
    → overenie stavu
    → malá zmena
    → publish + cache
    → kontrola, že platné ostalo platné
```

## Kedy ktorý príkaz

| Čo píšeš | Čo spustíš |
|---|---|
| „Chcem, aby…“ / otázka čo zmeniť / nápad | `/helpnisi-plan` |
| Schválený implementačný prompt z plánu | `/helpnisi-implement` |
| „Iba sa pozri, nič nemeň“ | bežný chat, bez MCP zápisu |
| Dokumentácia / rules v gite | plán, potom implementácia v gite (web sa nemení) |

Ak napíšeš zmenu webu bez `/helpnisi-plan`, agent má **najprv plánovať**, nie siahať na Elementor.

## Čo je schválenie

Schválenie je výslovné: „áno“, „schvaľujem“, „poď na to“, prípadne schválenie s úpravou („áno, a Kontakt v menu nech tiež ide na formulár“).

Mlčanie, „ok, znie to zaujímavo“ alebo nová nesúvisiaca veta **nie je** schválenie implementácie.

## Čo agent nikdy nesmie spojiť do jedného kroku

- plánovanie a publikovanie webu
- „ešte som si všimol a rovno som to opravil“
- veľký refactor „kým sme pri tom“

## Overenie (namiesto testov v gite)

Pri významnejšej zmene musí plán povedať:

1. **Čo sa má zmeniť** — jedna veta.
2. **Čo sa nesmie zmeniť** — okolité sekcie, texty, iné CTA.
3. **Ako overiť** — konkrétny klik / pohľad na desktop aj mobil, ak sa layout týka šírky.
4. **Čo spustiť** — tu nie sú unit testy. Typicky: `get-page-structure` po publish, curl/HTML kotvy, vizuálna kontrola živej URL.
5. **Používateľský scenár** — napr. „z headeru kliknem Dohodnúť konzultáciu a vidím formulár“.

Implementation Agent tento checklist vykoná. Ak MCP autentifikácia chýba, zastaví sa a povie to.

## Aktualizácia dokumentácie

Keď sa zmení fakt systému (nové ID, nová sekcia, nové pravidlo, vyriešená kotva), v tom istom kole sa upraví `docs/ai/`. Nenechávaj knowledge base za webom.

## Jazyk voči tebe

Planning Agent hovorí po slovensky, ľudsky. Technické ID a MCP volania patria do implementačného promptu, nie do prvého odseku návrhu.
