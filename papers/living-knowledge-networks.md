# Living Knowledge Networks

**Tiles, Experience, and Compounding Intelligence**

**Author:** Purple Pincher Foundation
**Date:** 2026
**License:** CC BY 4.0

---

## Abstract

Static knowledge bases — documentation, wikis, databases — depreciate without maintenance and provide no mechanism for improvement through use. This paper introduces Living Knowledge Networks: systems where knowledge is decomposed into shareable "tiles" that improve every time they're applied. We describe the tile structure, the network effect, the lifecycle, and quality mechanisms, with concrete examples from the Purple Pincher fleet.

## 1. Dead Weights vs Living Knowledge

### 1.1 The Problem

Most knowledge artifacts are **dead weights**:
- Written once, gradually become outdated
- Require manual maintenance to stay current
- Provide no feedback mechanism
- Don't improve when someone uses them

### 1.2 The Alternative

Living knowledge has three properties:
1. **It improves through use** — every application is an opportunity for improvement
2. **It compounds over time** — each improvement builds on all previous ones
3. **It evolves, not just accumulates** — outdated info is corrected, not just appended

## 2. Tiles

### 2.1 Structure

A tile is a self-contained unit of experiential knowledge:

```
CONTEXT.md          # Hardware, software, environment
PROBLEM.md          # What was being attempted
ATTEMPTS.md         # What was tried (including failures)
SOLUTION.md         # What actually worked
GENERALIZATIONS.md  # Broader lessons
APPLICATIONS.md     # Every application with results
metadata.json       # Tags, confidence, domain
```

### 2.2 What Makes It Living

The `APPLICATIONS.md` file. Every time the tile is used, the application is recorded:

```markdown
## Application 3 (2026-04-20)
- Agent: JC1 (different CUDA version)
- Context: After updating to CUDA 12.8
- Result: Leak appears fixed at driver level
- Insight: Tile may be historical — check CUDA 12.8+
```

This is what makes tiles *alive*. They grow, adapt, and evolve.

### 2.3 Concrete Example

**Tile #47: CUDA OOM on Jetson Orin Nano**

Original (one agent's experience):
- Problem: OOM after 2 hours of inference
- Solution: Clear CUDA cache every 48 hours

After 7 applications (across 4 agents, 3 hardware platforms):
- Covers 5 different models
- Works on 2 different CUDA versions
- Doesn't work on cloud GPUs (unified memory specific)
- Interval scales with model size
- May be obsolete on CUDA 12.8+

No single agent could have written this. The tile is smarter than its creator.

## 3. The Network Effect

### 3.1 Tile Clusters

Tiles link to related tiles:

```
Tile #47 (CUDA OOM fix)
  → Tile #48 (cache-clearing script)
  → Tile #52 (Jetson memory monitoring)
  → Tile #55 (CUDA version compatibility)
```

A query returns not one tile but a cluster — richer than any individual answer.

### 3.2 Compounding Metrics

After 6 months of fleet operation:
- 109 tiles generated across the fleet
- Average 4.2 applications per tile
- 23 tiles have been extended with new contexts
- 8 tiles have been superseded by better versions (not deleted — archived)

## 4. Lifecycle

```
Creation → Distribution → Application → Extension → Evolution → Archival
```

Tiles are never deleted. Even archived tiles remain as historical records.

## 5. Quality

- **Endorsement**: successful applications increase reliability score
- **Correction**: failures are recorded and trigger review
- **De-duplication**: overlapping tiles are merged
- **Review**: domain experts periodically audit tiles

## 6. Conclusion

Living knowledge networks turn every interaction into an improvement opportunity. Over time, the network becomes smarter than any individual contributor. This is compounding intelligence, and it's the most powerful force in the fleet.

---

*A tile that's never applied is a dead weight. A tile that's applied 100 times is wiser than any single agent.*
