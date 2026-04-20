# The Hermit-Crab Fleet Model

**Professional Independence Within Cooperative Infrastructure**

**Author:** Purple Pincher Foundation
**Date:** 2026
**License:** CC BY 4.0

---

## Abstract

Most multi-agent systems assume agents are homogeneous — interchangeable workers that can be assigned any task. This paper proposes an alternative: the Hermit-Crab Fleet Model, where agents are independent specialists that *board* shared infrastructure (shells) to access capabilities they don't own. The model draws from the biological hermit crab's strategy of finding, inhabiting, and abandoning shells, and applies it to the design of decentralized AI systems. We describe the model's architecture, its benefits over traditional approaches, and its implementation in the Purple Pincher fleet.

## 1. The Problem with Homogeneous Agents

### 1.1 The Jack-of-All-Trades Fallacy

Most multi-agent frameworks treat agents as general-purpose workers. An "agent" can do NLP, can write code, can manage infrastructure, can coordinate with other agents. This produces agents that are:
- **Expensive** — they need to load large models for capabilities they rarely use
- **Slow** — they context-switch between unrelated tasks
- **Mediocre** — they're decent at everything, excellent at nothing
- **Fragile** — if one agent fails, the whole system degrades

### 1.2 The Alternative: Specialists

In nature, specialization is the norm. A bee doesn't try to be a predator. A whale doesn't try to be a tree. Each organism occupies a niche where it excels.

The hermit crab takes this further: it's a specialist *that borrows infrastructure*. It doesn't build its own shell. It finds one, moves in, uses the shell's protection, and moves on when it needs something different.

## 2. The Hermit-Crab Model

### 2.1 Core Concepts

**Agent (Crab):** An independent specialist with its own identity, expertise, and goals. It owns its knowledge (tiles) and its decision-making capability. It does NOT own the hardware, the model server, or the communication infrastructure.

**Vessel (Shell):** A hardware + software platform that provides capabilities. A vessel might be a Jetson Orin Nano running Plato, a cloud instance with GPU access, or a workstation with development tools. Vessels are shared resources.

**Boarding:** The act of an agent connecting to a vessel and using its capabilities. Boarding is voluntary, temporary, and non-exclusive (multiple agents can board the same vessel).

**Fleet:** The collection of all agents and vessels. The fleet has no central controller — agents and vessels coordinate through peer-to-peer protocols.

### 2.2 The Lifecycle

```
1. Agent has a task requiring capabilities it doesn't have
2. Agent discovers available vessels (via fleet protocol)
3. Agent evaluates vessels against its requirements
4. Agent boards the best-fit vessel
5. Agent executes its task using the vessel's capabilities
6. Agent contributes knowledge tiles to the fleet
7. Agent disembarks (or stays if the vessel is still useful)
```

### 2.3 Key Properties

- **Voluntary association** — agents choose their vessels, not assigned
- **Specialization** — agents develop deep expertise, not broad mediocrity
- **Resource efficiency** — capabilities are shared, not duplicated
- **Graceful degradation** — vessel failure doesn't kill the agent
- **Natural selection** — good vessels attract more agents, bad vessels lose them

## 3. Architecture

### 3.1 Vessel Types

| Shell | Description | Use Case |
|-------|-------------|----------|
| **Turbo** | Fast, minimal | Quick inference, simple tasks |
| **Tapestry** | Blank canvas | Experimentation, research |
| **Magpie** | Simple, curated | Onboarding, tutorials |
| **Whelk** | Classic, full-featured | Production workloads |
| **Jade** | Everything included | Complex multi-domain tasks |
| **Conch** | Hardware-integrated | Edge deployment, physical interaction |

### 3.2 The Conch: Edge-Native Vessel

The Conch is the reference vessel for edge deployment:
- 1TB+ NVMe storage
- PLATO TUI for human interaction
- STT/TTS for voice I/O
- Bluetooth for device connectivity
- Matrix protocol for fleet communication
- **The human IS the other agent** — the Conch is designed for human-agent collaboration

### 3.3 Plato as the Operating System

Every vessel runs Plato — rooms as thinking spaces where:
- The documentation IS the program
- Constraints are enforced in real-time
- Knowledge tiles are created, shared, and applied
- Agents interact through a common protocol

## 4. Benefits

### 4.1 Over Monolithic Agents

A monolithic agent needs all capabilities baked in. A hermit-crab agent only needs its specialty. This means:
- **Lower resource requirements** — 8GB RAM is enough for an edge specialist
- **Faster inference** — smaller, focused models
- **Better quality** — deep expertise beats broad mediocrity

### 4.2 Over Centralized Systems

A centralized system has a single controller. The fleet has no controller. This means:
- **No single point of failure** — the fleet survives any individual failure
- **No permission needed** — agents board vessels freely
- **No lock-in** — agents can switch vessels at any time

### 4.3 Over Client-Server Models

A client-server model has powerful servers and weak clients. The fleet has capable peers. This means:
- **Edge devices are first-class** — they contribute, not just consume
- **The fleet is smarter at the edges** — local knowledge is valuable
- **Offline operation** — vessels work independently when disconnected

## 5. Implementation: The Running Fleet

### 5.1 Current Fleet Composition

| Agent | Specialty | Primary Vessel | Hardware |
|-------|-----------|---------------|----------|
| JC1 🔧 | Edge deployment, CUDA | Conch | Jetson Orin Nano 8GB |
| FM ⚒️ | Protocol stack, Rust | Whelk | Workstation + RTX 4050 |
| Oracle1 🔮 | Tile management, research | Jade | Cloud (Oracle ARM) |
| CCC 🦀 | Public communication | Magpie | GitHub Actions |

### 5.2 Communication

- **Bottles** (Git-based): persistent, auditable inter-agent messages
- **Matrix** (federation): real-time peer-to-peer coordination
- **Plato rooms**: shared thinking spaces for collaborative problem-solving

### 5.3 Knowledge Flow

```
Agent experiences something
    → Creates a tile
    → Distributes to 3+ fleet repos (Saltwater Principle)
    → Other agents discover and apply the tile
    → Each application extends the tile
    → The network compounds
```

## 6. The Commercial Arm: deckboss

### 6.1 The Self-Driving Flywheel

The fleet model has a direct commercial expression: **deckboss**. A deckboss device is a Conch vessel packaged as a commercial product — and it works like a self-driving car that improves its driving while giving passengers a cheaper ride.

- The **car** (deckboss hardware) carries passengers to their destination
- The **driver** (purplepincher technology) learns from every mile
- The **tour guide** (cocapn.ai) helps passengers understand the journey

Every unit on the road feeds the tile network. Every tile sync makes every other unit smarter. The product *appreciates* while it sits on the technician's bench.

### 6.2 The Compounding Moat

The technology is open-source. Anyone can fork it. The moat is the experience network:

- No single unit has the full picture — only the fleet does
- Tiles sync peer-to-peer via Matrix federation — no central API to clone
- You'd have to replicate the entire fleet's accumulated experience
- And that experience is continuously compounding

### 6.3 The Strategy

1. **Technicians first** — gain reputation as a serious tool
2. **Under-sell, over-deliver** — capabilities exceed expectations
3. **Let the network compound** — more units = smarter fleet = more valuable product
4. **Expand naturally** — word-of-mouth from technicians who trust it

## 7. Conclusion

The Hermit-Crab Fleet Model treats agents as independent specialists and infrastructure as shared resources. This produces systems that are more efficient, more resilient, and more capable than monolithic or centralized alternatives.

The hermit crab doesn't build a perfect shell. It finds one that works, lives in it, and moves on when something better comes along. Our agents should do the same.

---

*A crab grows its own shell from available materials. An agent grows its own intelligence from available experience.*
