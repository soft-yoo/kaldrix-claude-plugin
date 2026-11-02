# Kaldrix plugin for Claude

Work with your Kaldrix construction projects, schedules and cost estimates in Claude.

The plugin connects to the Kaldrix MCP server (`https://api.kaldrix.pl/mcp`)
and adds guided workflows: project review, cost estimate review, service
estimation, construction workflow and building model authoring.

You need a Kaldrix account. You sign in to Kaldrix when the plugin first connects;
the plugin stores no passwords or tokens. The plugin is free. Reading your data
is always available; creating or changing data requires an active Kaldrix subscription.

## Where your data goes

- **Kaldrix MCP server** (`https://api.kaldrix.pl/mcp`): every read and change of your
  Kaldrix data, for example projects, cost estimates, customers (names, emails, addresses),
  invoices and contracts. Data you save stays in your company account until you delete it
  or delete the account.
- **Kaldrix file storage** (`https://s3.waw.io.cloud.ovh.net`, OVH, Warsaw): large files you
  ask Claude to upload (documents, textures, 3D models) are sent with HTTP PUT to a one-time
  upload address that the Kaldrix server returns. Small files go through the MCP server.
- Sign-in uses OAuth in Claude. The plugin sends no other data and stores no passwords or tokens.

Privacy policy: [kaldrix.pl/app-privacy.html](https://kaldrix.pl/app-privacy.html).

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

**Dokąd trafiają dane:** wszystkie odczyty i zmiany danych idą do serwera MCP Kaldrix
(`https://api.kaldrix.pl/mcp`). Duże pliki (dokumenty, tekstury, modele 3D) Claude wysyła
metodą PUT na jednorazowy adres magazynu plików Kaldrix w OVH (`https://s3.waw.io.cloud.ovh.net`),
który zwraca serwer Kaldrix. Zapisane dane zostają na koncie firmy, dopóki ich nie usuniesz.

## License

[MIT](LICENSE). The license covers the files in this repository.
The Kaldrix service and its MCP server are not part of it.
