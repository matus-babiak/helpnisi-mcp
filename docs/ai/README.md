# Knowledge Base webu helpnisi

Toto je **zdroj pravdy** pre AI development. Ak sa niečo tu nezhoduje s `CLAUDE.md`, README alebo s pamäťou agenta, over aktuálny WordPress a túto zložku. Živý web je technická pravda o obsahu. Tento adresár je pravda o tom, ako má AI projekt rozvíjať.

## Čo tento projekt je

Nie je to klasická aplikácia so `src/`, databázou v repozitári a testami. Je to **pracovný repozitár k webu terapeutky** (značka helpnisi). Stránky žijú vo WordPresse. Tento git drží pravidlá, MCP konfiguráciu, podklady (obrázky) a túto knowledge base.

Vývojová adresa: https://helpnisi.matusbabiak.sk  
Repozitár: verejný. Heslá a `HELPNISI_MCP_AUTH` sem nikdy nepatria.

## Ako čítať tieto súbory

| Súbor | Účel |
|---|---|
| [product.md](./product.md) | Čo web robí, pre koho, flows, MVP, neznáme |
| [architecture.md](./architecture.md) | WordPress, Elementor, MCP, vrstvy, ako sa mení web |
| [content-map.md](./content-map.md) | Stránky, sekcie, médiá, formulár, obchod – namiesto dátového modelu |
| [business-rules.md](./business-rules.md) | Pravidlá, ktoré AI nesmie porušiť |
| [ui-ux.md](./ui-ux.md) | Dizajn: šírka, farby, písma, tlačidlá, animácie |
| [workflow.md](./workflow.md) | Ľudská veta → plán → schválenie → implementácia |
| [agent.md](./agent.md) | Čo robí Planning Agent a Implementation Agent |
| [harness.md](./harness.md) | Čo je nebezpečné a čo je zakázané |
| [analysis.md](./analysis.md) | Audit pôvodnej dokumentácie, konflikty, medzery |
| [golden-example.md](./golden-example.md) | Overený príklad plánovania na reálnom stave webu |

Nepoužívaj tieto súbory ako náhradu za kontrolu živej stránky. Pred návrhom zmeny vždy over aktuálny HTML/CSS alebo strom Elementoru.

## Ako spustiť agentov

V Cursore:

1. `/helpnisi-plan` — naplánuj zmenu. **Nič na webe neupravuj.**
2. Prečítaj návrh, odpovedz na otázky, schváľ alebo uprav.
3. `/helpnisi-implement` — až so schváleným implementačným promptom.

Bez schválenia sa web nemení.

## Pojmy

- **Hlavná priorita** — jedna vec v kole, zvyšok čaká.
- **Živý web** — publikovaný WordPress, nie draft v Elementore.
- **Repozitár** — git s pravidlami a podkladmi, nie zdroj stránok.

## Čo sem nepatrí

- Heslá, Application Passwords, hodnota `HELPNISI_MCP_AUTH`.
- Vymyslené produktové rozhodnutia.
- Všeobecný copy playbook. Texty na webe sú od klientky. Manuály na webové texty sem ešte neboli vložené (pozri [analysis.md](./analysis.md)).
