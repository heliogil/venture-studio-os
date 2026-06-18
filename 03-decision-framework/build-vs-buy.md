# Build vs Buy

Every infrastructure decision follows this framework.

## The rule

**Buy when:** the capability is not the moat.  
**Build when:** the capability is the moat, or the buy option is incompatible with the cost model.

## Applied examples

### Message queue (Redis vs file-based inbox)
**Decision: Build (file-based)**

Redis adds operational complexity (another service to monitor, failover to handle) for a problem that doesn't require it at our scale. A file-based inbox with `flock` is transparent, debuggable with `ls` and `cat`, and survives reboots without configuration.

**Revisit when:** > 100 concurrent packets or cross-machine distribution.

### LLM provider (OpenAI vs MiniMax vs Anthropic)
**Decision: Buy MiniMax flat-rate** (see [Flat-Rate LLM Strategy](flat-rate-llm-strategy.md))

### Benchmark data (HowManyFPS API vs proprietary pipeline)
**Decision: Build** for FPSReal

HowManyFPS charges $199–399/month for benchmark data. This is the exact data that is FPSReal's moat. Paying for it means the moat evaporates the moment a competitor pays the same price.

Build: triangulate from TechPowerUp + NanoReview + OpenBenchmarking. More work, but the normalised dataset becomes a proprietary asset.

### Payment processing (Stripe vs local gateway)
**Decision: Buy Stripe**

Payment is not the moat. Stripe's reliability, fraud protection, and global coverage are not worth building. The integration cost (a few hours) is trivially low.

### Auth (custom vs Clerk/Auth0)
**Decision: Build simple, buy when complex**

For internal tools (Nerve Center): custom JWT + TOTP. The user base is 1 person — zero reason to pay $25/month for Auth0.

For customer-facing products: Clerk or Supabase Auth once the user count justifies it.

### Scraping (Scrapy vs httpx)
**Decision: Build with httpx**

Scrapy is a framework for scraping at scale. Our scrapers are 50–100 line files per source. Scrapy's abstraction costs more to learn than to write the scraper directly. `httpx` + `BeautifulSoup` is readable by any Python developer and easier for Ergon to maintain.

**Revisit when:** > 20 sources or anti-bot requirements that need proxy rotation.

## The anti-pattern

**The worst decision:** buying a tool that is expensive and not the moat, then building workarounds when it doesn't fit.

Example: n8n for workflow orchestration. n8n is excellent for visual workflow building. It becomes a liability when the workflow logic is complex enough to need real code — you end up writing JavaScript inside a GUI instead of Python in a repo. We ported all n8n workflows to Python jobs in `scripts/jobs/`.
