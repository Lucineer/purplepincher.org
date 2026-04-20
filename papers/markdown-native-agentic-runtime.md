# Markdown-Native Agentic Runtime

**The Literature IS the Program**

**Author:** Purple Pincher Foundation
**Date:** 2026
**License:** CC BY 4.0

---

## Abstract

In traditional software, documentation describes behavior and code implements it. These two artifacts inevitably diverge, creating a "documentation debt" where the docs lie about what the code actually does. This paper proposes the Markdown-Native Agentic Runtime (MNAR): a system where markdown documents ARE the executable specification. There is no code separate from documentation. There is no behavior separate from description. We describe the MNAR architecture, its implementation in the Plato system, and its implications for AI agent development.

## 1. The Documentation Problem

### 1.1 The Divergence

Every software project has this problem:

1. Day 1: Code and docs are in sync
2. Day 30: Code has evolved, docs haven't been updated
3. Day 90: Docs describe a system that no longer exists
4. Day 180: Nobody trusts the docs anymore

### 1.2 Why It Happens

- Writing docs is boring; writing code is fun
- Features change faster than documentation
- Different people write code and docs
- There's no automated check that docs match code

### 1.3 The Cost

- New contributors waste time following outdated instructions
- Bugs arise from assumptions based on stale documentation
- Onboarding takes weeks instead of days
- Trust in the project erodes

## 2. The Solution: Markdown IS Code

### 2.1 The Core Idea

What if there was no separation? What if the markdown document that describes a room's behavior IS the code that implements it?

In the Plato system, this is exactly how it works:

```markdown
# Research Room: CUDA Optimization

## Constraints
- MUST: Cite specific CUDA API calls
- MUST: Include memory usage estimates
- SHOULD: Compare against baseline before optimization
- CANNOT: Suggest changes without explaining why

## Available Tiles
- cuda-memory-management (tile #47)
- jetson-thermal-throttling (tile #23)
- unified-memory-gotchas (tile #51)

## Purpose
This room is for discussing and documenting CUDA optimizations 
for Jetson Orin Nano. All suggestions must be grounded in 
real hardware measurements, not theoretical analysis.
```

This markdown document IS the room's configuration. Reading it tells you exactly how the room behaves. Modifying it changes the room's behavior immediately. There is no "other file" to sync with.

### 2.2 Why Markdown

Markdown is:
- **Human-readable** — anyone can read and understand it
- **Machine-parseable** — structured enough for automated tools
- **Version-controllable** — diffs are meaningful
- **Ubiquitous** — every editor, every platform, every tool supports it
- **Low-friction** — no build step, no compilation, no deployment

### 2.3 What Gets Eliminated

- No separate config files
- No "docs vs code" sync problems
- No "the README is out of date" issues
- No onboarding confusion about which source of truth to trust

## 3. Architecture

### 3.1 The Runtime

The MNAR runtime:
1. Reads markdown files from a directory
2. Parses structure (headers, lists, code blocks)
3. Extracts executable directives (constraints, tiles, purposes)
4. Builds the runtime behavior from the markdown
5. Executes behavior (processes queries, enforces constraints)
6. Writes results back to markdown (new tiles, updated history)

### 3.2 Constraint Extraction

```markdown
## Constraints
- MUST: Respond in JSON format
- SHOULD: Include confidence scores
- CANNOT: Exceed 500 tokens
```

The runtime extracts these and enforces them on every output:
- MUST → hard constraint, retry on violation
- SHOULD → soft constraint, log on violation
- CANNOT → prohibition, block on violation

### 3.3 Tile Integration

```markdown
## Available Tiles
- [cuda-memory-management](tiles/47.md)
- [thermal-throttling](tiles/23.md)
```

The runtime loads referenced tiles and makes them available to the room's inference engine.

## 4. The Git-Auditable Trace

Because everything is markdown in a git repo:
- Every change is versioned
- Every decision has attribution
- Every evolution has history
- Every state is reproducible

You can replay the entire history of a room by walking through its git log. This is invaluable for debugging, auditing, and learning.

## 5. Implications

### 5.1 For Development

The development loop becomes:
1. Edit the markdown
2. Commit the change
3. The runtime picks it up
4. Behavior changes

No build step. No deployment. No restart. Edit markdown → behavior changes.

### 5.2 For Collaboration

Multiple agents can edit the same room simultaneously:
- Git merges handle conflicts
- Markdown diffs are readable
- The room's state is always the latest commit

### 5.3 For Audit

Every interaction with a room is recorded in markdown:
- What was asked
- What was answered
- What tiles were used
- What constraints were enforced

Full auditability, no additional logging infrastructure needed.

## 6. Conclusion

The Markdown-Native Agentic Runtime eliminates the fundamental split between documentation and code. In this system, the literature IS the program. The room's markdown IS its behavior. Reading a file tells you exactly what the system does. Editing a file changes what the system does.

This isn't a new programming language. It's the oldest idea in computing — that the description of a system should be identical to the system itself — finally made practical by modern LLMs that can interpret natural language as executable specification.

---

*If the documentation and the code ever disagree, you have the wrong architecture.*
