# RoomieAI — Live Demo

An AI agent that handles shared-living commerce for PGs, flats, and joint families in India. Built on Swiggy's Food, Instamart, and Dineout MCPs.

**Submitted to:** Swiggy Builders Club — Developer Application
**Built by:** [Ramu Runja](https://github.com/Ramu-9346) · Hyderabad

---

## What this demo shows

Three fully playable scenarios that simulate how RoomieAI coordinates shared-living commerce through Swiggy's MCP APIs:

1. **Order dinner for the flat** — agent polls flatmates, aggregates preferences, builds a Swiggy Food cart, proposes the order, and shows UPI splits.
2. **Restock groceries** — agent analyzes past Instamart orders, proposes a consensus cart based on actual consumption patterns, and handles approval flow.
3. **Plan Saturday night** — agent surfaces Dineout options filtered by the flat's combined preferences, confirms availability, polls the group, and books.

All Swiggy interactions are **mocked** for this demo. The production build will swap the mock layer for real MCP tool calls — same interface, zero application logic change.

---

## Architecture (production build)

```
User (chat / WhatsApp)
    ↓
React + Vite frontend
    ↓
ASP.NET Core Web API  ←→  Claude (Anthropic API)
    ↓                          ↓
SQL Server              Swiggy MCPs (Food, Instamart, Dineout)
(flats, members,        + preference aggregation service
 orders, splits)
```

**Stack:**
- Backend: ASP.NET Core 8 Web API · 3-layer architecture (Controllers → Services → DAOs) · JWT auth · EF Core
- Database: SQL Server (structured state for flats, members, preferences, orders, splits)
- Agent: Claude via the Anthropic API · function-calling over Swiggy MCPs
- Frontend: React 18 + Vite · WhatsApp integration for group coordination
- Payments: UPI deep links (Swiggy handles order payment)

**Security:**
- OAuth-only sign-in (no password storage)
- Swiggy API keys in secrets manager, never in client code
- PII abstracted before any LLM call (only `Member A: veg, no peanuts` tags sent)
- Every order requires explicit group approval before placement

---

## Run locally

Just open `index.html` in any modern browser. No build step, no dependencies beyond Google Fonts.

```bash
# Clone and open
git clone https://github.com/Ramu-9346/roomie-ai-demo.git
cd roomie-ai-demo
open index.html     # macOS
# or: xdg-open index.html on Linux, start index.html on Windows
```

---

## Contact

**Ramu Runja**
📧 ramurunja91@gmail.com
💻 [github.com/Ramu-9346](https://github.com/Ramu-9346)
📍 Hyderabad, India
