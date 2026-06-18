# FPSReal

**PC hardware comparator for the Brazilian market — ranked by FPS per Real spent.**

## Identity

- **Tagline:** "FPS por Real."
- **Market:** Brazil — R$ pricing, KaBuM/Pichau/Terabyte/Mercado Livre affiliate links
- **Domain:** fpsreal.com.br (primary) + fpsreal.com (protection)
- **Positioning:** The only comparator that normalises by cost-efficiency, not raw performance

## What it does

- Compares GPUs, CPUs, and builds by FPS-per-Real in popular game titles
- Shows real Brazilian retail prices updated daily (KaBuM, Pichau, Terabyte, Mercado Livre)
- Recommends optimal builds by budget tier (R$2k / R$4k / R$8k)
- Flags price anomalies: "this GPU costs 40% more than its FPS output justifies"

## The moat

**Normalised, historised Brazilian hardware pricing.** BuildCores already commoditised 3D visualisation and airflow simulation globally. HowManyFPS sells benchmark API access at $199–399/month. Neither offers:
1. Brazilian retail price tracking (R$ with local merchant URLs)
2. Historical price trends (has this GPU ever been cheaper?)
3. Cost/FPS as the primary ranking dimension

The data pipeline — scraping 4+ merchants, normalising SKU names, triangulating benchmarks — becomes a proprietary asset that compounds.

## Stack

| Layer | Tech |
|---|---|
| Database | PostgreSQL (port 5434, isolated from Sharp) |
| Ingestion API | FastAPI (port 8100) |
| Web | Next.js (port 3100) |
| Benchmark data | Triangulated: TechPowerUp + NanoReview + OpenBenchmarking |
| Price scraping | httpx + BeautifulSoup, 4 merchants |
| Affiliates | KaBuM, Pichau, Terabyte, Mercado Livre (post-approval), Amazon |
| 3D viewer | Three.js (launch, kill switch at week 5 if <400 fresh SKUs) |

## Business model

Affiliate commission on every click that converts. R$0.5k–5k/month year 1 (media/SEO business, not SaaS).

## State (as of 2026-06-18)

Sprint 1 in progress:
- PCB-101: monorepo scaffold (in queue)
- PCB-102: 9-table schema (in queue)
- PCB-103: seed data — 12 GPUs, 3 CPUs, 4 boards, 4 merchants (in queue)
- PCB-104: Mercado Livre adapter (blocked — awaiting ML Developers token)
- PCB-105: benchmark pipeline (in queue)

Pending founder actions: ML Developers token, domain purchase, Pichau affiliate registration.

## Kill criteria (90 days post-launch)

- < 500 affiliate clicks → archive
- 0 media/creator coverage (100k+ reach) → review, not automatic archive
- Both → archive immediately

Gate: B-event launch (full product at once, not gradual rollout).
