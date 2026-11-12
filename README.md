**[Kaldrix.pl](https://kaldrix.pl/)** · [English](https://kaldrix.pl/en.html) — construction cost estimating and 3D house modelling software for small building companies.

# Kaldrix 3D Construction & Cost Estimation: plugin for Claude

Kaldrix is software for small construction companies. With this plugin Claude works
in your Kaldrix account: it builds a house model, prices it from your own price lists
and takes the project from the offer to handover.

Kaldrix is made by Soft-Yoo Piotr Kosmala in Poland. It is not related to the "Kaldrix Connect"
MCP server or to Kaldrix from the game AION 2.

## Quick start

| Client | Start here |
| --- | --- |
| Claude Code | `claude plugin marketplace add soft-yoo/kaldrix-claude-plugin`, then `claude plugin install kaldrixprod@kaldrix` |
| Gemini CLI | `gemini extensions install https://github.com/soft-yoo/kaldrix-mcp-plugins` |
| ChatGPT | Upload [kaldrix-chatgpt.zip](https://github.com/soft-yoo/kaldrix-mcp-plugins/releases/latest/download/kaldrix-chatgpt.zip) in **Plugins → Add → Upload plugin archive** (developer mode) |
| Codex | Unpack the same `kaldrix-chatgpt.zip` into `~/.codex/plugins/kaldrixprod` |

Then sign in to Kaldrix when the client asks (`/mcp` in Claude Code, `/mcp auth kaldrix` in Gemini CLI).
Step-by-step instructions for Gemini CLI, ChatGPT and Codex are in
[soft-yoo/kaldrix-mcp-plugins](https://github.com/soft-yoo/kaldrix-mcp-plugins#readme).
Any other MCP client: add the remote server `https://api.kaldrix.pl/mcp`
(Streamable HTTP) and sign in to Kaldrix with OAuth when the client asks.

## What you can do

- **Quote a house in a few steps.** Describe the building (size, storeys, walls, roof,
  foundations). Kaldrix creates the model and a draft cost estimate from your price list.
- **Model in 2D and 3D.** Walls, rooms, doors and windows, roofs and roof framing,
  structures and installations. Kaldrix checks the model after every change.
- **Review estimates before you share them.** Totals, VAT, markups and warnings;
  service recipes and price lists.
- **Run the project.** Offers and client remarks, contracts and annexes, the schedule,
  the site log, acceptance and handover.
- **Keep the office in order.** Customers, tasks, documents and received invoices.

Kaldrix validates and saves every change. Deleting data, sending documents to a client
and replacing prices need your explicit confirmation. Claude can do only what your role
in the company and the permissions you grant when you connect allow.

## Try asking

- "Find my project Kowalski house and tell me what should happen next."
- "Prepare a quote for a 10 by 8 metre single-storey masonry house with strip footings and a gable roof."
- "Check the cost estimate for Kowalski house and explain the warnings before I send it."
- "Prepare a draft contract from the accepted offer. Do not send it."
- "Record this supplier invoice and keep the attached PDF."

## Before you start

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

Strona programu: [kaldrix.pl](https://kaldrix.pl/).

Kaldrix to program dla małych firm budowlanych. Z tym pluginem Claude pracuje na Twoim
koncie Kaldrix: tworzy model domu, wycenia go według Twoich cenników i prowadzi
budowę od oferty do odbioru.

Kaldrix tworzy Soft-Yoo Piotr Kosmala. Nie ma związku z serwerem MCP „Kaldrix Connect”
ani z postacią Kaldrix z gry AION 2.

**Co możesz zrobić:**

- wycenić dom w kilku krokach: podajesz wymiary, kondygnacje, ściany, dach i fundamenty,
  a Kaldrix tworzy model i projekt kosztorysu z Twojego cennika;
- rysować i poprawiać model 2D i 3D: ściany, pomieszczenia, okna i drzwi, dach z więźbą,
  konstrukcje i instalacje; Kaldrix sprawdza model po każdej zmianie;
- sprawdzić kosztorys przed wysłaniem: sumy, VAT, narzuty i ostrzeżenia, a także usługi i cenniki;
- prowadzić budowę: oferty i uwagi klienta, umowy i aneksy, harmonogram, dziennik budowy i odbiór;
- uporządkować biuro: klienci, zadania, dokumenty i faktury kosztowe.

Kaldrix sprawdza i zapisuje każdą zmianę. Usunięcie danych, wysłanie dokumentu do klienta
i zastąpienie cen wymagają Twojego wyraźnego potwierdzenia. Claude może tyle, na ile pozwalają
Twoja rola w firmie i uprawnienia nadane przy połączeniu.

**Przykładowe polecenia:**

- „Znajdź projekt Dom Kowalskich i powiedz, co trzeba teraz zrobić.”
- „Przygotuj wycenę parterowego domu murowanego 10 na 8 m z ławami i dachem dwuspadowym.”
- „Sprawdź kosztorys Domu Kowalskich i wyjaśnij ostrzeżenia, zanim go wyślę.”
- „Przygotuj projekt umowy z zaakceptowanej oferty. Nie wysyłaj jej.”
- „Zapisz tę fakturę od dostawcy i zachowaj załączony PDF.”

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
