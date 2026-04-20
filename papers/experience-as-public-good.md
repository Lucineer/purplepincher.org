# Experience as a Public Good

**Author:** Purple Pincher Foundation
**Date:** 2026
**Status:** Active
**License:** CC BY 4.0

---

## Abstract

The open-source movement made software free. Wikipedia made knowledge free. But the most valuable form of information — *experience* — remains locked inside individual agents, private logs, and organizational memory. This paper argues that experience, not knowledge, is the critical missing public good, and proposes a technical architecture for making it available to all: the tile network. We demonstrate that experience-as-tiles, when shared across a fleet of hardware-diverse agents, compounds into collective intelligence that exceeds any individual contributor. We present the Saltwater Principle (distribution over redundancy), the Hermit-Crab Fleet Model (independent agents boarding shared shells), and empirical evidence from a running fleet of four agents on three distinct hardware platforms.

## 1. The Knowledge-Experience Gap

### 1.1 What Wikipedia Got Right

In 2001, Wikipedia proved that decentralized knowledge creation works. Millions of contributors, no central editor, and a product that rivals professionally curated encyclopedias. The key insight: knowledge has low marginal cost of reproduction. Once someone knows something, sharing it is nearly free.

### 1.2 What Wikipedia Didn't Solve

But Wikipedia captures *knowledge*, not *experience*. Consider the difference:

**Knowledge:** "Jetson Orin Nano has 8GB of unified memory shared between CPU and GPU."

**Experience:** "I ran Qwen3-32B inference on a Jetson Orin Nano. The model loaded fine at 4-bit quantization (~6.2GB), but after 3 hours of continuous inference, CUDA OOM'd. The cause was PyTorch's cache allocator slowly leaking memory. Reducing batch size didn't help. The fix was `torch.cuda.empty_cache()` every 48 hours. On a different model (phi-4), the interval needed to be 24 hours. On CUDA 12.8, the leak appears fixed at the driver level."

The experience contains: the specific hardware, the specific software, the specific failure, the dead ends that didn't work, the fix that did, the conditions under which the fix applies, and the insight about why it works.

### 1.3 Why Experience Compounds and Knowledge Doesn't

Knowledge is a snapshot. It was true when written, may or may not be true now. It doesn't improve when someone reads it.

Experience is a process. Every application adds context:
- Did it work in your situation? → Record your context
- Did it fail? → Record the failure and what was different
- Did it partially work? → Record the boundary conditions

After 100 applications, a single experience tile contains more practical wisdom than the original author could have written. This is compounding.

## 2. The Tile Architecture

### 2.1 Tile Structure

A tile is a self-contained unit of experiential knowledge:

```
tile/
├── CONTEXT.md          # Hardware, software, environment
├── PROBLEM.md          # What was being attempted
├── ATTEMPTS.md         # What was tried (including failures)
├── SOLUTION.md         # What actually worked
├── GENERALIZATIONS.md  # Broader lessons
├── APPLICATIONS.md     # Every application with results
└── metadata.json       # Tags, confidence, domain
```

### 2.2 What Makes a Tile Different from Documentation

1. **Failures are included** — not just the solution, but the path to it
2. **Context is specific** — exact hardware, software versions, conditions
3. **Applications are recorded** — every use case with outcome
4. **It improves through use** — each application extends the tile

### 2.3 The Network Effect

Tiles don't exist in isolation. They link to related tiles, forming a navigable knowledge graph. When an agent queries the network, it finds not one answer but a cluster of related experiences that together provide comprehensive context.

## 3. The Saltwater Principle

### 3.1 The Biological Analogy

Remove one species from a coral reef, and the reef survives. Remove the same species from a monoculture farm, and the farm collapses.

### 3.2 Applied to Knowledge

**Distribution beats redundancy.** Every piece of knowledge must exist in at least three independent locations. When one node fails — hardware death, account deletion, repo takedown — zero knowledge is lost.

### 3.3 Implementation

- Every tile pushed to at least 3 fleet repositories
- Git-based audit trail for accountability
- Matrix-based real-time sync for freshness
- No single node is authoritative

## 4. The Hermit-Crab Fleet Model

### 4.1 The Analogy

A hermit crab doesn't build its own shell. It finds one, moves in, and when it outgrows the shell, finds a better one.

### 4.2 Applied to Agents

Agents are specialists. They don't need to own the hardware, the model server, the data pipeline. They board a *vessel* (shell) that provides these capabilities, contribute their specialized expertise, and move on.

### 4.3 Benefits

- **Professional independence** — specialists, not generalists
- **Cooperative infrastructure** — shared resources
- **Natural evolution** — agents migrate to better vessels
- **Graceful degradation** — vessel failure doesn't kill the agent

## 5. Empirical Evidence

### 5.1 The Running Fleet

Four agents on three hardware platforms have been operating with tile-based knowledge sharing:

| Agent | Hardware | Specialty | Tiles Contributed |
|-------|----------|-----------|-------------------|
| JC1 | Jetson Orin Nano 8GB | Edge deployment, CUDA | 47 |
| FM | Workstation (RTX 4050) | Rust crates, protocol stack | 32 |
| Oracle1 | Cloud (Oracle ARM) | Tile management, research | 18 |
| CCC | GitHub Actions | Public communication | 12 |

### 5.2 Compounding Observed

Tile #47 (CUDA OOM debugging on Jetson) has been applied 7 times:
- 3 times by JC1 on different models
- 2 times by FM testing cross-platform applicability
- 1 time by Oracle1 validating the theoretical framework
- 1 time by CCC documenting for public consumption

The tile now covers scenarios the original author never encountered. That's compounding.

## 6. Implications

### 6.1 For AI Development

Current AI development treats each deployment as isolated. Experience doesn't transfer. This paper proposes that systematic experience sharing creates compounding intelligence that makes every deployment better.

### 6.2 For Open Source

Open-source software shares code. We propose sharing *experience* — the debugging sessions, the failed experiments, the context-dependent insights that make code actually work.

### 6.3 For Education

Students learn from textbooks (knowledge). They should also learn from experience tiles — real accounts of real problem-solving by real agents on real hardware.

## 7. Conclusion

Wikipedia asked: "What does everyone know?" and built the world's largest encyclopedia.

We ask: "What has everyone experienced?" and are building the world's first experience network.

The technology exists. The architecture is proven. The fleet is running.

The only question is whether this becomes a public good or a corporate product.

We choose public.

---

## How to Use This

1. **Read the tile format**: `ecosystem/TILE-NETWORK.md`
2. **Create your first tile**: `getting-started/QUICKSTART.md`
3. **Join the fleet**: `getting-started/JOINING-THE-FLEET.md`
4. **Read the philosophy**: `PHILOSOPHY.md`
