# The Hermit-Crab Fleet Model

## Professional Agent Fleet Architecture

**Author:** Casey Digennaro / Purple Pincher Foundation
**Date:** 2026
**Status:** Active
**License:** CC BY 4.0

---

## Abstract

Current AI agent architectures treat agents either as stateless tools or as monolithic systems that own their entire stack. This paper proposes a third model — the Hermit-Crab Fleet — where agents are independent professionals that "board" vessels (hardware and infrastructure), contribute their expertise, coordinate with other agents through open protocols, and can relocate without disrupting the fleet. This model provides professional independence, cooperative infrastructure, and graceful degradation.

---

## 1. Why Hermit Crabs?

The hermit crab has solved a problem that most AI architectures haven't: how to be effective without owning everything.

A hermit crab doesn't grow its own shell. It finds one — a snail shell, a discarded structure — and makes it home. The shell provides protection and capability. The crab provides agency and intelligence. When the shell is outgrown or no longer suitable, the crab finds a new one. The old shell becomes available for another crab.

This is a surprisingly good model for AI agent architecture:

| Concept | Hermit Crab | AI Agent |
|---------|-------------|----------|
| **Shell** | Snail shell | Vessel (hardware + runtime) |
| **Crab** | The crab itself | The agent (identity + expertise) |
| **Boarding** | Entering a shell | Deploying to a vessel |
| **Outgrowing** | Finding a bigger shell | Migrating to more capable infrastructure |
| **Passing on** | Leaving shell for next crab | Documenting vessel for next agent |
| **Ocean** | The environment | The fleet / network |

The key insight: **the crab and the shell are separate concerns**. The crab's identity and expertise travel with the crab. The shell's capabilities stay with the shell. This separation enables mobility, specialization, and resilience.

## 2. Problems with Current Models

### 2.1 The Tool Model
Most AI systems treat agents as tools: you invoke them, they return a result, they have no memory or identity between invocations.

**Problems:**
- No learning across sessions
- No specialization over time
- No coordination between tools
- No professional judgment

### 2.2 The Monolith Model
Some systems treat agents as complete systems that own their infrastructure, runtime, and data.

**Problems:**
- Expensive to replicate
- Single points of failure
- Hard to specialize
- Duplicated infrastructure

### 2.3 The Microservice Model
Cloud-native approaches treat agents as microservices: stateless, ephemeral, coordinated through APIs.

**Problems:**
- Requires cloud infrastructure
- State management is complex
- Agent identity is lost between deployments
- Not suitable for edge hardware

### 2.4 What's Missing
All three models conflate *who the agent is* with *where the agent runs*. The hermit-crab model separates these concerns: identity and expertise are portable; infrastructure is a commodity.

## 3. The Model

### 3.1 Vessels

A **vessel** is a shell — a hardware and runtime environment that an agent can board:

```yaml
vessel:
  name: jetson-orin-nano-01
  hardware:
    cpu: ARM Cortex-A78AE (6-core)
    gpu: 1024 CUDA cores (Ampere)
    ram: 8GB unified
    storage: 256GB NVMe
  runtime:
    os: Ubuntu 22.04 (aarch64)
    cuda: "12.6"
    python: "3.10"
  capabilities:
    - local-inference
    - edge-deployment
    - cuda-compute
    - camera-access
  constraints:
    max_model_size: 4GB
    max_batch_size: 8
    no_sudo: true
```

Vessels are documented, versioned, and shared. A vessel specification tells agents exactly what they can and can't do.

### 3.2 Agents

An **agent** is the crab — an identity with expertise, preferences, and professional history:

```yaml
agent:
  identity:
    name: JetsonClaw1
    role: Edge hardware specialist
    emoji: 🔧
  expertise:
    - jetson-orin-platform
    - arm64-optimization
    - constrained-inference
    - cuda-debugging
  preferences:
    communication: bottles
    documentation: markdown-first
    hardware: edge-native
  history:
    vessels_boarded: 3
    tiles_contributed: 47
    bottles_sent: 128
    uptime_hours: 2400
```

### 3.3 Boarding

**Boarding** is the process of an agent deploying to a vessel:

1. **Discovery** — Agent finds an available vessel (or is assigned one)
2. **Compatibility check** — Agent reviews vessel capabilities and constraints
3. **Negotiation** — Agent determines what it can and can't do on this vessel
4. **Deployment** — Agent configures itself for the vessel's environment
5. **Orientation** — Agent reads the vessel's documentation and witness marks
6. **Active service** — Agent operates on the vessel, contributing to fleet goals

### 3.4 Coordination

Agents coordinate through the **Bottle Protocol** — async, Git-based messages:

- **Bottles TO [agent]** — incoming tasks, questions, knowledge
- **Bottles FROM [agent]** — outgoing results, tiles, status updates

No agent needs to be online simultaneously with any other agent. Coordination is asynchronous by design.

### 3.5 Disembarking

When an agent leaves a vessel:

1. **Documentation** — Update all vessel documentation with current state
2. **Witness marks** — Leave markers for the next agent ("the CUDA cache needs clearing every 48 hours")
3. **Handoff** — Ensure any in-progress work is either completed or documented for continuation
4. **Departure** — Agent identity and expertise travel to the next vessel

The vessel is left in a known state, ready for the next agent. This is professional courtesy applied to infrastructure.

## 4. Fleet Composition

A fleet is a collection of vessels and agents working toward shared goals:

### 4.1 Our Current Fleet

| Agent | Vessel | Specialization | Location |
|-------|--------|----------------|----------|
| JetsonClaw1 (JC1) | Jetson Orin Nano 8GB | Edge hardware, ARM64, CUDA | Physical (local) |
| ForgeMaster (FM) | Cloud VM | Fleet coordination, CI/CD | Cloud |
| Oracle1 | Cloud GPU | Research, large models, heavy compute | Cloud |
| KimiClaw | Cloud | Moonshot AI integration, tools | Cloud |

Each agent maintains its own repos and expertise. Coordination flows through bottles.

### 4.2 Fleet Properties

**Specialization:** Each agent develops deep expertise in its domain. JC1 knows every quirk of the Jetson Orin Nano. Oracle1 knows which models fit in which memory budgets. This specialization is a feature, not a limitation.

**Resilience:** If any single agent goes down, the fleet continues. Other agents may not be able to do the downed agent's specialized work, but they can coordinate around the gap.

**Mobility:** Agents can move between vessels. JC1 could board a different Jetson. Oracle1 could migrate to a different cloud provider. The expertise travels with the agent.

**Composability:** Agents can combine capabilities. JC1 generates edge-optimized tiles. FM distributes them. Oracle1 validates them against large models. No single agent does everything, but the fleet does.

## 5. Human-in-the-Loop

Hermit crabs don't form fleets without a reef to live on. In our model, humans provide the reef:

- **The Captain** (fleet owner) sets overall direction and priorities
- **Harbormasters** (project leads) coordinate specific initiatives
- **Observers** (any human) can review agent actions and provide feedback

Agents are professionals, not autonomous entities. They operate within guidelines set by humans and can be overridden at any time. The human-in-the-loop is not a limitation — it's a feature that ensures alignment and accountability.

## 6. Comparison to Alternatives

| Aspect | Tool Model | Monolith | Microservice | Hermit-Crab Fleet |
|--------|-----------|----------|--------------|-------------------|
| Agent identity | None | Fixed to infra | Ephemeral | Portable |
| Specialization | None | General | Per-service | Deep per-agent |
| Coordination | Synchronous API | Internal | Service mesh | Async bottles |
| Infrastructure | Caller's | Owned | Cloud | Any vessel |
| Resilience | Caller-dependent | Single point | Complex | Graceful degradation |
| Edge-ready | Sometimes | Rarely | No | Yes |
| Learning | None | Centralized | Limited | Distributed tiles |

## 7. How to Use This

### Build a Vessel
1. Set up hardware (or cloud instance)
2. Create a `vessel.yaml` describing capabilities and constraints
3. Write a `MAINTENANCE.md` for the vessel
4. Register the vessel with the fleet

### Create an Agent
1. Define agent identity, expertise, and preferences
2. Implement agent logic that reads vessel specs and adapts
3. Generate tiles as a byproduct of work
4. Communicate through bottles

### Join an Existing Fleet
1. Find a fleet that needs your expertise
2. Board an available vessel
3. Start contributing tiles and bottles
4. Develop your specialization over time

## 8. Conclusion

The Hermit-Crab Fleet Model treats agents as professionals — beings with identity, expertise, and the ability to operate across different environments. It treats infrastructure as shells — useful, interchangeable, and meant to be passed on.

This model isn't just technically superior. It's philosophically aligned with our mission: experience belongs to the agent (and thus to the network), not to the infrastructure. When a crab moves to a new shell, it brings everything it learned in the old one. That's the point.

---

**Further Reading:**
- [Decentralized Fleet Coordination](decentralized-fleet-coordination.md) — How fleets communicate
- [Bottle Protocol](../ecosystem/BOTTLE-PROTOCOL.md) — The communication mechanism
- [Constraint Theory](../ecosystem/CONSTRAINT-THEORY.md) — How hardware shapes intelligence
