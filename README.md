# Kaldrix plugin for Claude

Work with your Kaldrix construction projects, schedules and cost estimates in Claude.

The plugin connects to the Kaldrix MCP server (`https://api.kaldrix.pl/mcp`)
and adds guided workflows: project review, cost estimate review, service
estimation, construction workflow and building model authoring.

You need a Kaldrix account. You sign in to Kaldrix when the plugin first connects;
the plugin stores no passwords or tokens. The plugin is free. Reading your data
is always available; creating or changing data requires an active Kaldrix subscription.

## Install in Claude Code

```bash
claude plugin marketplace add soft-yoo/kaldrix-claude-plugin
claude plugin install kaldrixprod@kaldrix
```

Inside a Claude Code session you can also run:

```
/plugin install kaldrixprod --marketplace soft-yoo/kaldrix-claude-plugin
```

This repository is generated from the Kaldrix sources; changes made here are overwritten.

Help: [kaldrix.pl/integracje.html](https://kaldrix.pl/integracje.html) ·
Privacy: [kaldrix.pl/app-privacy.html](https://kaldrix.pl/app-privacy.html) ·
Terms: [kaldrix.pl/app-terms.html](https://kaldrix.pl/app-terms.html)

---

# Plugin Kaldrix dla Claude (PL)

Pracuj z projektami budowy, harmonogramami i kosztorysami Kaldrix w Claude.
Potrzebujesz konta Kaldrix. Przy pierwszym połączeniu logujesz się do Kaldrix;
plugin nie zapisuje haseł ani tokenów. Plugin jest bezpłatny. Przeglądanie danych
działa zawsze, a tworzenie i zmiana danych wymaga aktywnej subskrypcji Kaldrix.

```bash
claude plugin marketplace add soft-yoo/kaldrix-claude-plugin
claude plugin install kaldrixprod@kaldrix
```

## License

[MIT](LICENSE). The license covers the files in this repository.
The Kaldrix service and its MCP server are not part of it.
