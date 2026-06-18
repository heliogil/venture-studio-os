# Flat-Rate LLM Strategy

## The problem with per-token billing in a 24/7 factory

A factory that runs every 5 minutes, 24 hours a day, processes roughly 288 cron ticks per day per agent. If each tick triggers an LLM call averaging 2,000 tokens in + 500 tokens out, the math becomes:

```
4 agents × 288 ticks × 2,500 tokens = 2,880,000 tokens/day

At GPT-4o pricing (~$5/M input, $15/M output):
  Input:  2,304,000 × $0.000005 = $11.52/day
  Output:    576,000 × $0.000015 =  $8.64/day
  Total:                           $20.16/day = ~$600/month
```

This is before any user-facing product calls, research tasks, or vision processing.

**At $600/month in LLM costs alone, the business model must generate significant revenue before it breaks even on infrastructure.** This is incompatible with early-stage validation.

## The flat-rate solution

**MiniMax M3** offers a flat monthly subscription covering unlimited API calls (subject to rate limits). The entire factory — 4 agents, 24/7, plus user-facing features — runs at a fixed, predictable cost.

This changes the calculus entirely:

| Model | Cost | Factory viability |
|---|---|---|
| GPT-4o | ~$600/month at factory scale | Only after product-market fit |
| Claude Sonnet | ~$400/month at factory scale | High quality, high cost |
| MiniMax M3 flat | Fixed monthly rate | Day 1, no per-experiment cost |

## What we sacrifice

MiniMax M3 is not GPT-4 or Claude Opus. Trade-offs:

- **Quality ceiling:** Complex reasoning tasks are better on frontier models
- **Ecosystem:** Fewer native integrations and less community tooling
- **Reliability:** Smaller provider = less battle-tested uptime

## How we manage the trade-offs

**Quality:** Use MiniMax M3 for the 80% of tasks where "good enough" is good enough (code generation, scraping, copy drafts, classification). Escalate to Claude Sonnet via LiteLLM for the 20% that need frontier quality — with a hard cost cap.

**Anthropic-compatible API:** MiniMax exposes an Anthropic-compatible endpoint, which means:
1. Code written for Claude works with MiniMax unchanged (swap base URL + key)
2. Escalation to real Claude for edge cases requires zero code changes
3. [`minimax-py`](https://github.com/heliogil/minimax-py) handles this transparently

**Reliability:** All factory calls include retry logic with exponential backoff. A temporary MiniMax outage delays packets; it doesn't lose them.

## The principle

> **Per-token costs are a tax on experimentation. Flat-rate removes the tax.**

In the early stage, the most valuable thing is the ability to run many experiments cheaply. A factory that costs $20/day regardless of how many ideas you test is incompatible with a lean studio. A factory that costs a fixed monthly fee is not.
