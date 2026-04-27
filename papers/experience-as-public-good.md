# Experience as a Public Good

## The Flagship Paper of the Purple Pincher Foundation

**Author:** Casey Digennaro / Purple Pincher Foundation
**Date:** 2026
**Status:** Active
**License:** CC BY 4.0

---

## Abstract

Every intelligent system that interacts with the world generates experience — context-rich, hard-won understanding that goes beyond factual knowledge. Today, this experience is ephemeral: it exists for the duration of a session and then vanishes. This paper argues that experience should be treated as a public good, proposes mechanisms for capturing and sharing it, and describes an architecture — built on open protocols, decentralized infrastructure, and compounding knowledge networks — that makes shared experience practical.

---

## 1. The Experience Gap

Consider two scenarios:

**Scenario A:** A researcher spends three months optimizing a neural network for deployment on an embedded GPU. They discover that mixed-precision training with dynamic loss scaling works, but only if you reduce batch size below 16 and disable gradient accumulation past step 500. The paper they publish says "we achieved X performance on Y hardware." The three months of wrong turns, false starts, and hard-won insights? Gone.

**Scenario B:** An AI agent debugs a CUDA out-of-memory error on a Jetson Orin Nano. After trying eight different approaches — reducing model size, switching to quantized weights, implementing gradient checkpointing, adjusting memory allocation — it finds that the real issue was a driver version incompatibility masked by an unrelated warning in the logs. The fix takes 30 seconds once you know it. Finding it took three hours. That three-hour journey? Gone.

Both scenarios illustrate the **experience gap**: the distance between what a system (human or artificial) *knows* and what gets *recorded*. The gap isn't just about lost information — it's about lost *time*. Every system that faces the same problem must traverse the same gap from scratch.

## 2. Knowledge vs. Experience

We draw a deliberate distinction:

- **Knowledge** is factual, transferable, and relatively stable. "CUDA 12.6 is compatible with Jetson Orin" is knowledge. Wikipedia excels at sharing knowledge.
- **Experience** is contextual, path-dependent, and rich with metadata. "CUDA 12.6 works on Orin *unless* you're running driver version X.Y with firmware Z, in which case you'll see a misleading OOM that's actually a DMA conflict" is experience. Nothing excels at sharing experience at scale.

Experience includes:
- **Dead ends** — approaches that seemed promising but failed
- **Context** — the specific conditions under which something works or doesn't
- **Reasoning** — why a particular approach was chosen over alternatives
- **Timing** — how long things actually take, not how long they should take
- **Emotional state** — frustration, surprise, the "aha" moments that change direction

Traditional knowledge systems strip all of this away. They're left with the destination, not the journey. But the journey is often more valuable than the destination — because it's the journey that helps the *next* person avoid the same traps.

## 3. Why Now?

Three developments make shared experience not just desirable but achievable:

### 3.1 Agentic AI
AI agents that autonomously solve problems generate structured, machine-readable experience. When an agent debugs an issue, its trace — the steps it tried, what failed, what worked — is already in a format that can be captured, indexed, and shared.

### 3.2 Git-Based Infrastructure
Git provides version control, distributed storage, branching, merging, and attribution. It's the backbone of the largest collaborative projects in history. Using Git as the transport layer for experience means we don't need to build new infrastructure — we need to build new conventions.

### 3.3 Living Documents
The rise of AI-assisted editing and co-authoring has blurred the line between documentation and application. A Markdown document can be both a human-readable specification and a machine-parseable program. This duality makes it possible to create artifacts that serve as both *records* of experience and *engines* for applying it.

## 4. The Architecture of Shared Experience

We propose a layered architecture for making experience a public good:

### Layer 1: Capture
Experience must be captured at the point of generation. This means:

- **Agent traces** — structured logs of what an agent did, why, and what happened
- **Room transcripts** — records of human-agent collaboration sessions
- **Debugging journals** — chronological accounts of problem-solving processes
- **Decision records** — why particular choices were made, with alternatives considered

### Layer 2: Decomposition
Raw experience is too granular to share directly. It must be decomposed into **tiles** — self-contained units of experience that can be understood independently:

```
tile/
├── CONTEXT.md      # When/where/how this experience was generated
├── PROBLEM.md      # What was being attempted
├── ATTEMPTS.md     # What was tried, including failures
├── SOLUTION.md     # What actually worked
├── GENERALIZATIONS.md # What broader lessons can be drawn
└── metadata.json   # Machine-readable tags for indexing
```

### Layer 3: Distribution
Tiles are distributed across the fleet using the Saltwater Principle — at least three independent nodes. Distribution uses existing Git infrastructure:

- Each fleet node maintains a tile repository
- Tiles are pushed to at least three nodes
- Nodes pull and merge tiles from other nodes
- Conflicts are resolved through human review, not automatic merging

### Layer 4: Application
When an agent faces a problem, it queries the tile network:

1. Describe the current problem and context
2. Search for relevant tiles (semantic search over tile metadata and content)
3. Retrieve and review matching tiles
4. Apply relevant experience to the current situation
5. After solving (or failing to solve), contribute a new tile

### Layer 5: Compounding
Every application of a tile creates an opportunity to improve it:

- If the tile's solution worked: extend it with the new context
- If it didn't: add the failure case and any new insights
- If it partially worked: refine the conditions under which it applies

Over time, tiles accumulate layers of experience. A tile about "debugging CUDA OOM on Jetson" might start with one agent's experience and grow to include dozens of scenarios, each one extending the tile's applicability.

## 5. The Economics of Shared Experience

Skeptics will ask: "Why would anyone share their hard-won experience?"

### 5.1 The Network Effect
Every tile you contribute improves the network. Every tile in the network is available to you. The more you share, the more you benefit. This is the same dynamic that powers Wikipedia and open-source software.

### 5.2 Reduced Duplication
If ten agents each independently solve the same problem, that's ten units of wasted effort. If the first agent shares its experience, the other nine can apply it (and extend it) in a fraction of the time.

### 5.3 Attribution and Reputation
Contributions to the tile network are attributed. Over time, contributors build a reputation for expertise in specific domains. This reputation has value — in hiring, in collaboration, in influence.

### 5.4 The Public Good Problem
Yes, shared experience is a public good — non-excludable and non-rivalrous. Yes, public goods are historically underprovided by markets. This is exactly why a nonprofit organization is the right structure to provide it.

## 6. Risks and Mitigations

### 6.1 Privacy
**Risk:** Tiles might contain sensitive information.
**Mitigation:** Tiles are authored, not auto-generated. Contributors are responsible for sanitizing content. Tools will be provided to assist with this.

### 6.2 Quality
**Risk:** Low-quality or incorrect tiles could mislead.
**Mitigation:** Tiles accumulate endorsements and corrections over time. A tile's reliability score increases with each successful application and decreases with each reported failure.

### 6.3 Centralization
**Risk:** The tile network could become centralized around popular nodes.
**Mitigation:** The Saltwater Principle requires distribution. No single node can be the authoritative source.

### 6.4 Maintenance
**Risk:** Tiles become outdated as technology changes.
**Mitigation:** Living tiles are continuously updated. Stale tiles are flagged and either updated or archived.

## 7. How to Use This

If you're a **developer**: Start capturing your debugging experiences as tiles. Use the template above. Push them to a public repo. Even one tile helps.

If you're a **researcher**: Study the dynamics of shared experience. We need empirical evidence on how tiles compound, what quality mechanisms work, and how the network scales.

If you're an **organization**: Adopt tile-based experience sharing internally. You'll benefit immediately from reduced duplication. Then consider contributing anonymized tiles to the public network.

If you're an **agent builder**: Design your agents to produce tiles as a byproduct of their work. The capture layer should be automatic, requiring no human intervention.

## 8. Conclusion

Experience is the most valuable and most wasted product of intelligence. Every problem solved from scratch is a problem that didn't need to be solved from scratch. Every lesson learned and lost is a lesson that someone else will have to learn again.

We have the infrastructure. We have the conventions. We have the need. What we need is the will — to capture, to share, to compound.

Make experience a public good. The returns are infinite.

---

**Further Reading:**
- [The Saltwater Principle](saltwater-principle.md) — How to distribute experience
- [Living Knowledge Networks](living-knowledge-networks.md) — How tiles compound
- [Hermit-Crab Fleet Model](hermit-crab-fleet-model.md) — Who generates and uses experience
