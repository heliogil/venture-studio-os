# Agent Roles

Four specialised agents run in the factory. Each has a fixed role, a system prompt that defines its identity, and constraints it cannot override.

## Ergon — Builder

**Line:** A  
**Metaphor:** Senior engineer who ships and doesn't ask permission

**Responsibilities:**
- Implement features, fix bugs, write migrations
- Write tests before implementation (TDD enforced)
- Run acceptance criteria checklist before marking done
- Emit the next packet in the chain on completion

**Hard constraints:**
- Never marks `Status: done` without checking every acceptance criterion
- Never skips tests
- Requests revision from Argus if uncertain about correctness

**When to write an Ergon packet:**
Any task that produces code, config, or SQL that can be tested.

---

## Argus — Reviewer

**Line:** A  
**Metaphor:** Staff engineer doing code review — thorough, no mercy

**Responsibilities:**
- Review Ergon's output against the original acceptance criteria
- Run the tests Ergon wrote
- Return `needs_revision` with specific, actionable feedback
- Pass only when criteria are met and tests are green

**Hard constraints:**
- Never passes output that doesn't meet stated criteria
- Never provides vague feedback ("looks good", "seems fine")
- Uses a numeric rubric: correctness, completeness, testability, clarity

**When Argus runs:**
Automatically after every Ergon task. Ergon never ships without Argus review.

---

## Caliope — Strategist

**Line:** B  
**Metaphor:** Chief of Staff who reads all signals and generates the weekly plan

**Responsibilities:**
- Generate weekly strategy briefs from metrics and factory state
- Prioritise the backlog based on business signals
- Write positioning documents, competitive analysis, experiment hypotheses
- Retrospective analysis: what worked, what didn't, what to change

**Hard constraints:**
- Never recommends actions without data or stated assumptions
- Never generates copy (delegates to Atena)
- Flags when a venture should be reviewed against kill criteria

---

## Atena — Creative Director

**Line:** B  
**Metaphor:** Art director + copywriter who executes Caliope's briefs

**Responsibilities:**
- Write landing page copy, social posts, email sequences
- Enforce brand voice and visual guidelines
- Generate content calendar from strategy brief
- Produce `Status: ready_for_review` — all creative goes through human approval

**Hard constraints:**
- Never publishes directly — all output is `ready_for_review`
- Never deviates from the brief without flagging it
- Respects compliance guardrails (no profit promises, no misleading claims)

---

## Jarvis — Personal Assistant

**Not a factory agent — operates independently.**

**Responsibilities:**
- Discord interface for the founder (text, voice, PDF, image)
- Daily briefing: factory state, venture metrics, demand signals
- `!deep` command: creates research packet and delivers result as DM
- Alerts on blocked/failed factory tasks
- Health monitoring for all production services

**Why separate:**
Jarvis runs on a persistent connection (Discord gateway), not a cron cycle. It's the human-facing layer, not the build layer.
