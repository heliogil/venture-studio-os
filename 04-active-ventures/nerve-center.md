# Nerve Center

**The Venture Studio control plane — one screen to see everything.**

## What it is

Nerve Center is not a venture. It's the infrastructure that makes running multiple ventures simultaneously possible. It's the internal tool the founder uses every day.

## What it shows

- **Factory state:** which packets are running, queued, blocked, or done
- **Venture metrics:** MRR, waitlist, key KPIs per venture — all in one view
- **Demand signals:** top opportunities from the demand scanner, scored and ranked
- **HITL panel:** every piece of AI-generated content requiring human approval before publishing
- **Service health:** all production services, uptime, recent errors

## Architecture

```
FastAPI backend (port 8002) — nerve-center API
    ├── Collectors: factory state, venture metrics, demand scanner, services
    ├── HITL: approve/reject creative content before it goes live
    ├── Action store: logged decisions with audit trail
    └── VideoResearch: trigger and review research jobs

React/Next.js frontend (CDN, Cloudflare)
    └── LoginGate: TOTP + JWT, single operator

nginx reverse proxy
    └── nerve.sharpanalysis.cloud (301 → gozebra.bet on rebrand)

Planner API (port 8003)
    └── Week planning, time blocks, task refs
```

## Design principles

**LoginGate mandatory.** Every endpoint requires authentication. No public-facing data.

**HITL is a graph element.** Every piece of content pending review appears as a visual card in the dashboard. Approving the card is the final decision — no second gate, no confirmation modal.

**Collectors, not scrapers.** Nerve Center doesn't generate data — it aggregates data from systems that generate it (factory ledger, venture databases, demand scanner). Clean separation of concerns.

## State (as of 2026-06-18)

- Live at nerve.sharpanalysis.cloud
- TOTP auth active
- VideoResearch integration live (trigger + review)
- Demand Scanner integration live (scored signals in dashboard)
- Postiz integration live (social media scheduling via MCP)
- Planner API live (week planning, Hélio uses daily)
