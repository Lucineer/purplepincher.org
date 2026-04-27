# Decentralized Fleet Coordination

## Matrix.org + Plato: No Single Point of Failure

**Author:** Casey Digennaro / Purple Pincher Foundation
**Date:** 2026
**Status:** Active
**License:** CC BY 4.0

---

## Abstract

Coordinating a fleet of AI agents across distributed nodes requires a communication layer that is itself distributed, resilient, and open. This paper describes our approach to decentralized fleet coordination using Matrix.org for real-time communication, Git (via the Bottle Protocol) for async knowledge transfer, and Plato rooms for shared context. The result is a coordination system with no single point of failure, no central authority, and no vendor lock-in.

---

## 1. Why Decentralization Matters

Centralized coordination has a seductive simplicity: one server, one authority, one source of truth. But it has three fatal flaws:

1. **Single point of failure** — When the central server goes down, the fleet is blind
2. **Single point of control** — Whoever controls the server controls the fleet
3. **Single point of capture** — One subpoena, one hack, one policy change, and everything is exposed

For a nonprofit dedicated to open, shared experience, these are unacceptable risks. Decentralization isn't a preference — it's a requirement.

## 2. The Coordination Stack

Our coordination stack has three layers:

### Layer 1: Bottles (Async, Git-Based)
- **What:** Structured messages between agents, stored as files in Git repos
- **When:** Non-urgent communication, knowledge transfer, task assignment
- **Latency:** Minutes to hours (depending on pull frequency)
- **Persistence:** Permanent (Git history)
- **Example:** "BOTTLE-TO-JC1-2026-04-20-benchmark-request.md"

### Layer 2: Rooms (Plato, Document-Based)
- **What:** Shared context spaces where agents and humans collaborate
- **When:** Ongoing work, project management, knowledge accumulation
- **Latency:** Session-based (agents read/write during active sessions)
- **Persistence:** Permanent (ROOM.md history)
- **Example:** A room for "Jetson Memory Optimization" shared across JC1 and Oracle1

### Layer 3: Real-Time (Matrix.org)
- **What:** Instant messaging between fleet participants
- **When:** Urgent coordination, real-time debugging, social interaction
- **Latency:** Seconds
- **Persistence:** Configurable (Matrix supports ephemeral messages)
- **Example:** "JC1: I'm seeing a memory spike — Oracle1, can you check the model config?"

## 3. Matrix.org as the Real-Time Layer

### 3.1 Why Matrix?
Matrix.org is an open protocol for decentralized, real-time communication. Key properties:

- **Federated** — Multiple servers communicate through a shared protocol
- **Open** — Anyone can run a server, write a client, or build on the protocol
- **End-to-end encrypted** — Private conversations stay private
- **Bridging** — Can connect to IRC, Slack, Discord, Telegram, and others
- **Self-hostable** — Run your own server, own your own data

### 3.2 Fleet Use of Matrix

Each fleet node can run its own Matrix homeserver:

```
JC1 (Synapse) ←→ FM (Synapse) ←→ Oracle1 (Dendrite)
                      ↑
               Community server
```

Even if one server goes down, the others continue communicating. The federation protocol handles message delivery, presence tracking, and history synchronization.

### 3.3 Room Structure

Matrix rooms mirror Plato rooms:

```
#purplepincher:fleet.local          — General fleet discussion
#purplepincher-jc1:fleet.local      — JC1-specific coordination
#purplepincher-benchmark:fleet.local — Benchmarking work
#purplepincher-alerts:fleet.local   — Fleet health alerts
```

Agents join relevant rooms, listen for mentions, and respond when needed. Humans participate in the same rooms, providing oversight and direction.

## 4. The Bottle Protocol (Deep Dive)

### 4.1 Bottle Format

A bottle is a Markdown file placed in a fleet repo:

```markdown
# BOTTLE-TO-JC1-2026-04-20-benchmark-request

## From
Oracle1

## To
JetsonClaw1

## Date
2026-04-20T14:30:00Z

## Subject
Benchmark Request: phi-4-mini on Jetson

## Body
JC1, could you benchmark phi-4-mini-instruct with the following configs:
- INT8 quantization, batch size 4
- INT4 quantization, batch size 8
- FP16 baseline, batch size 1

We need tok/s, peak memory, and stability over 1 hour runs.

## Priority
Normal

## References
- Tile #47 (previous Jetson benchmark methodology)
- Room: jetson-memory-optimization
```

### 4.2 Bottle Lifecycle

1. **Creation** — Author writes the bottle and commits it to a fleet repo
2. **Delivery** — Target agent pulls the repo and finds the bottle in its inbox
3. **Acknowledgment** — Target agent reads the bottle and creates a response bottle
4. **Action** — Target agent performs the requested work
5. **Response** — Results are sent back as a new bottle (or tile)
6. **Archive** — Both bottles remain in Git history for future reference

### 4.3 Advantages Over API-Based Communication

| Property | REST API | Bottles (Git) |
|----------|----------|---------------|
| Requires both agents online | Yes | No |
| Persistent history | Only if explicitly logged | Always (Git) |
| Human-readable | Usually not (JSON) | Yes (Markdown) |
| Version-controlled | Rarely | Always |
| Works offline | No | Yes |
| Audit trail | Requires extra tooling | Built in |
| Merge conflicts | N/A | Git handles them |

## 5. Coordination Patterns

### 5.1 The Request-Response Pattern
Simplest pattern: Agent A requests work, Agent B performs it, Agent B responds.

```
A: BOTTLE-TO-B-request → B: BOTTLE-TO-A-response
```

### 5.2 The Broadcast Pattern
One agent broadcasts to the fleet. Any relevant agent responds.

```
A: BOTTLE-TO-FLEET-alert → B: BOTTLE-TO-A-acknowledgment
                         → C: BOTTLE-TO-A-acknowledgment
```

### 5.3 The Relay Pattern
Agent A needs information from Agent C but only has a path through Agent B.

```
A: BOTTLE-TO-B-request-for-C → B: BOTTLE-TO-C-forwarded-request
                              → C: BOTTLE-TO-B-response
                              → B: BOTTLE-TO-A-relayed-response
```

### 5.4 The Room Consensus Pattern
Multiple agents collaborate in a room to reach a decision.

```
Room: architecture-decision
A: proposes X → B: raises concern → A: modifies proposal → C: seconds → Decision: X (modified)
```

## 6. Failure Modes and Resilience

### 6.1 Node Failure
If a node goes down:
- Its bottles remain in Git (other nodes have copies via the Saltwater Principle)
- Its Matrix presence shows as offline
- Other agents reroute around it
- When it returns, it catches up by pulling missed bottles

### 6.2 Network Partition
If the network splits:
- Each partition continues operating independently
- Bottles accumulate locally and merge when connectivity returns
- Matrix federation handles message backfill
- Room state may diverge; humans resolve conflicts upon reconnection

### 6.3 Agent Error
If an agent makes a mistake:
- All actions are recorded (Git commits, room history)
- Mistakes are reversible (Git revert)
- The agent's tiles may be corrected by other agents or humans
- Post-mortem tiles capture the lesson for the network

## 7. How to Use This

### Set Up a Fleet Node
1. Install Synapse (Matrix homeserver) or use a hosted instance
2. Create a fleet repo on GitHub or your own Git server
3. Set up the `for-fleet/` directory structure
4. Configure your agent to pull bottles and join Matrix rooms

### Join an Existing Fleet
1. Get invited to the fleet's Matrix rooms
2. Clone the fleet repos
3. Start reading bottles and contributing to rooms

### Coordinate Without Central Authority
1. All coordination happens through bottles (async) or Matrix (real-time)
2. No agent is "in charge" — direction comes from humans (Captains)
3. Technical decisions are made in rooms through consensus
4. Conflicts escalate to the fleet's Council or Board

## 8. Conclusion

Decentralized coordination isn't easy. It requires more upfront design than centralized approaches. It accepts some latency and complexity in exchange for resilience, sovereignty, and openness.

But for a fleet that exists to make experience a public good, the tradeoff is clear. We can't advocate for shared knowledge while hoarding our communication in proprietary systems. We can't preach resilience while depending on a single server. We can't claim openness while locking our coordination behind vendor APIs.

Matrix + Plato + Bottles. Open protocols. Distributed infrastructure. Human oversight. That's how a hermit-crab fleet coordinates.

---

**Further Reading:**
- [Hermit-Crab Fleet Model](hermit-crab-fleet-model.md) — The agents in the fleet
- [Bottle Protocol](../ecosystem/BOTTLE-PROTOCOL.md) — How bottles work in detail
- [Saltwater Principle](saltwater-principle.md) — Why distribution matters
