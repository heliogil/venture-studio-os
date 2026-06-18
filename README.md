# Venture Studio OS

A documented operating system for building AI ventures — from idea to market in 6–8 weeks, with a factory that runs 24/7 and a decision framework that kills bad bets before they get expensive.

This is the methodology behind [Zebra Shield](https://github.com/heliogil/sharpanalysis), [FPSReal](https://github.com/heliogil/fpsreal), and the [Nerve Center](https://github.com/heliogil/nerve-center-showcase) control plane.

## Contents

### [01 — The Factory](01-factory/)
How AI agents do the build work. Ephemeral Docker executors, multi-pass TDD, automatic reviewer, closer loop.

- [How it works](01-factory/how-it-works.md)
- [Packet protocol](01-factory/packet-protocol.md) — the unit of work
- [Agent roles](01-factory/agent-roles.md) — who does what
- [Factory cycle](01-factory/factory-cycle.md) — cron to shipped result

### [02 — Venture Lifecycle](02-venture-lifecycle/)
How a venture moves from idea to gate to launch or archive.

- [Experiment criteria](02-venture-lifecycle/experiment-criteria.md) — what earns a sprint
- [Kill criteria](02-venture-lifecycle/kill-criteria.md) — what gets archived
- [Gate metrics](02-venture-lifecycle/gate-metrics.md) — the 90-day scorecard
- [Sprint structure](02-venture-lifecycle/sprint-structure.md) — how weeks are organised

### [03 — Decision Framework](03-decision-framework/)
The principles behind every stack and strategic decision.

- [Build vs buy](03-decision-framework/build-vs-buy.md)
- [Flat-rate LLM strategy](03-decision-framework/flat-rate-llm-strategy.md)
- [Stack defaults](03-decision-framework/stack-defaults.md)

### [04 — Active Ventures](04-active-ventures/)
Current ventures with stack, state, and next milestone.

- [Zebra Shield](04-active-ventures/zebra-shield.md) — bankroll intelligence, EN-first
- [FPSReal](04-active-ventures/fpsreal.md) — PC hardware comparator, BR market
- [Nerve Center](04-active-ventures/nerve-center.md) — studio control plane

## Philosophy

**The factory runs always.** The founder's job is to write good packets and read good results — not to execute every task manually.

**One experiment at a time.** Each venture is a market experiment with a defined gate. Parallel ventures create divided attention and muddled signals.

**Kill criteria before you build.** Every venture has a written kill condition before the first line of code. This removes emotion from the decision.

**Flat-rate or nothing.** Per-token LLM costs are incompatible with a 24/7 factory. Every model in production runs on flat-rate pricing.

---

Built by [Hélio Gil](https://github.com/heliogil) — AI venture builder based in Brazil.
