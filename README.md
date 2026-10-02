# helpnisi-mcp

Pracovný repozitár k webu **helpnisi** (WordPress + Elementor): podklady, konfigurácia MCP, knowledge base a pravidlá pre AI agentov.

Obsah webu je vo WordPresse na https://helpnisi.matusbabiak.sk. Tento git slúži na to, aby sa na webe dalo pracovať z viacerých zariadení s rovnakým kontextom a s oddeleným plánovaním od implementácie.

## Ako dávať prácu AI

Napíš ľudsky, čo chceš. Potom:

1. `/helpnisi-plan` — agent overí web a navrhne najmenšiu zmenu. Nič nepublikuje.
2. Schváliš (alebo upresníš).
3. `/helpnisi-implement` — agent zmenu urobí, publikuje, overí.

Zdroj pravdy: [`docs/ai/README.md`](docs/ai/README.md).

## Čo tu je

| Súbor / priečinok | Na čo slúži |
|---|---|
| `docs/ai/` | Knowledge base a AI workflow |
| `.cursor/commands/` | `/helpnisi-plan`, `/helpnisi-implement` |
| `.cursor/rules/` | Pravidlá, ktoré Cursor berie vždy |
| `CLAUDE.md` | Krátky vstup + MCP pasce |
| `AGENTS.md` | Vstup pre Cursor |
| `.mcp.json` | MCP pre Claude Code |
| `.cursor/mcp.json` | MCP pre Cursor |
| `.env.example` | Vzor pre prihlasovací údaj |
| `images/` | Fotky a grafika (podklady) |

## Prihlasovací údaj

Repozitár je verejný, preto v ňom nie je žiadne heslo. Konfiguračné súbory čítajú `HELPNISI_MCP_AUTH`.

Hodnota je reťazec za slovom `Basic` v prompte, ktorý vygeneruje Elementor (WP admin → Elementor → MCP). Je to base64 z `pouzivatel:aplikacne-heslo` bez medzier.

### Windows (PowerShell, natrvalo)

```powershell
[Environment]::SetEnvironmentVariable("HELPNISI_MCP_AUTH", "SEM_VLOZ_RETAZEC", "User")
```

Potom reštartuj Cursor / terminál.

### macOS / Linux

```bash
echo 'export HELPNISI_MCP_AUTH="SEM_VLOZ_RETAZEC"' >> ~/.zshrc
```

### Claude na mobile / na webe

V nastaveniach cloudového prostredia pridaj premennú `HELPNISI_MCP_AUTH` a do povolených domén doplň `helpnisi.matusbabiak.sk`. Bez povolenej domény sa cloudová relácia na web nepripojí.

## Ako začať

1. Naklonuj repozitár a nastav `HELPNISI_MCP_AUTH`.
2. Otvor priečinok v Cursore alebo v Claude Code.
3. Zmenu webu spusti cez `/helpnisi-plan`.

## Pravidlo pre každú úpravu webu

1. naplánovať a schváliť,
2. upraviť cez MCP,
3. publikovať dokument,
4. vyčistiť cache Elementoru,
5. skontrolovať živú stránku,
6. ak sa zmenil systémový fakt, dopísať `docs/ai/` a commitnúť.
