# helpnisi-mcp

Pracovný repozitár k webu **helpnisi** (WordPress + Elementor): podklady, konfigurácia MCP a pravidlá pre AI agentov.

Samotný obsah webu je vo WordPresse na https://helpnisi.matusbabiak.sk a upravuje sa cez MCP server Elementoru. Tento repozitár slúži na to, aby sa na webe dalo pracovať z viacerých zariadení a nástrojov s rovnakým kontextom.

## Čo tu je

| Súbor / priečinok | Na čo slúži |
|---|---|
| `CLAUDE.md` | Kontext projektu, pravidlá dizajnu, overené postupy. Číta ho Claude. |
| `AGENTS.md` | To isté v skratke pre Cursor a iných agentov. |
| `.mcp.json` | Pripojenie MCP pre Claude Code. |
| `.cursor/mcp.json` | Pripojenie MCP pre Cursor. |
| `.env.example` | Vzor pre prihlasovací údaj. |
| `images/` | Fotky a grafika použité na webe. |

## Prihlasovací údaj

Repozitár je verejný, preto v ňom nie je žiadne heslo. Oba konfiguračné súbory čítajú premennú prostredia `HELPNISI_MCP_AUTH`.

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
2. Otvor priečinok v Cursore alebo v Claude Code – server `template-elementor` sa načíta z konfigurácie v repozitári.
3. Zadaj úlohu. Agent si pravidlá prečíta z `CLAUDE.md` / `AGENTS.md`.

## Pravidlo pre každú úpravu webu

1. upraviť cez MCP,
2. publikovať dokument,
3. vyčistiť cache Elementoru,
4. skontrolovať živú stránku.

Keď sa zmení niečo podstatné (nová sekcia, nové pravidlo, nové ID), dopíš to do `CLAUDE.md` a commitni.
