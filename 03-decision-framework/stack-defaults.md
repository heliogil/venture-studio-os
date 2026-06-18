# Stack Defaults

These are the defaults for every new venture unless there's a specific reason to deviate.

## Backend

| Layer | Default | Why |
|---|---|---|
| Language | Python 3.12 | Factory agents write Python natively; broadest AI library ecosystem |
| API framework | FastAPI | Async, auto-docs, Pydantic validation, Ergon knows it well |
| Database | PostgreSQL | Reliable, extensible (pgvector for embeddings), single instance shared across ventures |
| Cache / dedup | Redis | Separate DB index per venture (DB 2, 3, 4...) |
| Background jobs | Python cron + file bus | No Celery, no broker — see [Build vs Buy](build-vs-buy.md) |
| Auth | Custom JWT + TOTP | Internal tools; Clerk for customer-facing at scale |
| Containerisation | Docker Compose | Single VPS, no Kubernetes until the scale justifies it |

## Frontend

| Layer | Default | Why |
|---|---|---|
| Framework | Next.js 14 (App Router) | React ecosystem, SSR for SEO-sensitive ventures |
| Styling | Tailwind CSS | Ergon generates Tailwind reliably; consistent with Nerve Center design system |
| State | React Query + local state | No Redux unless explicitly needed |
| Deploy | CDN (Cloudflare Pages / Vercel) | Static-first, zero config, global edge |

## Infrastructure

| Layer | Default | Why |
|---|---|---|
| VPS | Contabo (single instance) | Flat-rate, EU-based, sufficient for early-stage multi-venture |
| Reverse proxy | nginx | Stable, well-documented, Ergon can configure it |
| SSL | Let's Encrypt via certbot | Free, automated |
| DNS | Cloudflare | Free tier, DDoS protection, fast propagation |
| Monitoring | Jarvis health checks + UptimeRobot | Alerts before users notice |
| Secrets | Environment variables via systemd | No Vault, no AWS Secrets Manager at this scale |

## AI / LLM

| Layer | Default | Why |
|---|---|---|
| Primary model | MiniMax M3 | Flat-rate — see [Flat-Rate LLM Strategy](flat-rate-llm-strategy.md) |
| Escalation model | Claude Sonnet via LiteLLM | Cap: $1/day hard limit |
| STT | Whisper (local) | Free, private, sufficient quality |
| Embeddings | MiniMax embeddings | Same flat-rate subscription |
| Vector store | pgvector | Already have PostgreSQL; no separate Pinecone cost |

## Deviate from defaults when

- The venture's moat IS the technology (then build something custom)
- A specific constraint makes the default impossible (e.g., mobile-first requires React Native)
- The cost structure at scale changes the equation (e.g., PostgreSQL → PlanetScale if global distribution is the product)

Document every deviation and the reason. Undocumented deviations become technical debt.
