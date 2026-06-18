# Factory Cycle

How a packet moves from idea to delivered result inside the venture factory.

## The Cycle

```mermaid
sequenceDiagram
    participant O as Operator
    participant I as Inbox
    participant S as Scheduler (cron)
    participant C as Container (docker --rm)
    participant X as Outbox
    participant H as HITL Gate

    O->>I: drop packet.json (state=queued)
    S->>I: poll every 5 min
    S->>C: docker run --rm agent-image < packet.json
    C->>C: understand → plan → execute
    C->>X: write result.json
    S->>X: pick up result
    alt needs_revision
        S->>I: re-queue with feedback
    else blocked
        S->>H: surface to HITL panel
        H->>I: operator approves / redirects
    else done
        S->>O: notify + archive
    end
```

## Packet States

```mermaid
stateDiagram-v2
    [*] --> queued: packet dropped in inbox
    queued --> running: scheduler picks up
    running --> done: result accepted
    running --> needs_revision: reviewer rejects (< 3 rounds)
    running --> blocked: reviewer rejects (3rd round) OR missing context
    needs_revision --> queued: re-queued with feedback
    blocked --> queued: operator resolves via HITL
    done --> [*]: archived
```

## Rules

| Rule | Detail |
|------|--------|
| One agent per flock | `flock -n` on agent line prevents parallel double-runs |
| Ephemeral containers | `docker run --rm` — no state leaks between packets |
| Max 3 revision rounds | After round 3, packet goes to `blocked`, not back to `queued` |
| HITL = visual gate | Every blocked packet surfaces on the Nerve Center panel; approval there is final — no second confirmation |
| Kill criterion | Stop spending on an agent line when: cost is ongoing AND no active signal from that line |

## File Layout

```
/opt/factory/
  inbox/          # operator drops packets here
  outbox/         # agent writes results here
  archive/        # scheduler moves done packets here
  logs/           # one log per packet execution
  agents/         # agent definitions (one dir per agent)
    builder/
    reviewer/
    closer/
  scheduler.py    # cron entry point
```

## Adding a New Agent

1. Create `agents/<name>/run.py` — reads `packet.json` from stdin, writes result to stdout
2. Add a line to `scheduler.py` pointing at the new agent dir
3. Drop a test packet in `inbox/` and watch `outbox/`

No restart needed — the scheduler picks up new agent dirs on the next cron tick.
