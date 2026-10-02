# Pokyny pre AI agentov

Zdroj pravdy: [`docs/ai/README.md`](docs/ai/README.md). Operatívne MCP pasce: [`CLAUDE.md`](./CLAUDE.md).

## Workflow

1. `/helpnisi-plan` — pochop, over živý web, navrhni, spýtaj sa, počkaj na schválenie. Web nemente.
2. Až potom `/helpnisi-implement` so schváleným zadaním.

V jednom kole jedna **hlavná priorita**. Texty na webe sú od klientky. Heslá do gitu nepatria. Obsah stránok žije vo WordPresse a mení sa cez MCP `template-elementor`, nie cez `src/`.
