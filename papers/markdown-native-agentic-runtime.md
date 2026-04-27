# Markdown-Native Agentic Runtime

## The Literature of the Program IS the Program

**Author:** Casey Digennaro / Purple Pincher Foundation
**Date:** 2026
**Status:** Active
**License:** CC BY 4.0

---

## Abstract

Traditional software development separates code from documentation — the code does the work, the documentation describes it. We propose inverting this relationship: the documentation IS the program. In a Markdown-native agentic runtime, human-readable Markdown documents serve simultaneously as specification, documentation, configuration, and execution context for AI agents. This approach reduces drift between code and docs, makes programs inspectable by humans and machines alike, and creates artifacts that compound in value over time.

---

## 1. The Documentation Problem

Every software engineer has experienced this:

1. You read the documentation. It says the function does X.
2. You call the function. It does Y.
3. You read the source code. It does Z.
4. The documentation was written two years ago. The code has changed six times since.

This is **documentation drift** — the gap between what docs say and what code does. It's universal, expensive, and largely unsolved. Tools like Swagger, JSDoc, and docstrings help, but they treat documentation as a *derivative* of code: generate it, hope it stays current, accept that it won't.

The Markdown-native agentic runtime takes the opposite approach: **make the documentation the source of truth, and let agents derive behavior from it.**

## 2. The Core Idea

> *The literature of the program IS the program.*

In a traditional runtime:

```
Source Code → Compiler → Binary → Execution → (Documentation is separate)
```

In a Markdown-native runtime:

```
Markdown Document → Agent reads it → Agent acts according to the document →
Document is updated with results → Loop
```

The Markdown document contains:

- **Purpose** — What this program/room/agent is supposed to do
- **Rules** — Constraints, boundaries, and operating procedures
- **State** — Current status, active tasks, known issues
- **History** — What's been tried, what worked, what didn't
- **Knowledge** — Tiles, references, and accumulated experience

The agent reads the document, interprets it, acts accordingly, and updates it with results. The document IS the program state.

## 3. Why Markdown?

### 3.1 Human-Readable
Markdown is the closest thing we have to a universal format for structured text. Any human can read it. Any text editor can edit it. No special tools required.

### 3.2 Machine-Parseable
Markdown has a well-defined structure (headers, lists, code blocks, links) that agents can parse and reason about. It's not as precise as JSON or YAML, but that imprecision is a feature — it allows natural language where precision isn't needed.

### 3.3 Version-Controllable
Git handles Markdown beautifully. Diffs are readable. Merges are (usually) clean. History is preserved. The entire version control ecosystem works with Markdown out of the box.

### 3.4 Composable
Markdown files can link to each other, embed code blocks, include images, and reference external resources. A collection of Markdown files can represent a complete system — not just its documentation.

### 3.5 Ubiquitous
GitHub renders it. VS Code previews it. Every messaging platform supports some variant. There are no compatibility issues, no proprietary formats, no vendor lock-in.

## 4. How It Works

### 4.1 The AGENTS.md Pattern

In the OpenClaw ecosystem, the entry point for any workspace is `AGENTS.md`:

```markdown
# AGENTS.md - Workspace Configuration

## Session Startup
Before doing anything else:
1. Read SOUL.md - who you are
2. Read USER.md - who you're helping
3. Read memory/YYYY-MM-DD.md for recent context

## Red Lines
- Don't exfiltrate private data
- Don't run destructive commands without asking
- trash > rm
```

An agent reads this file at the start of every session. It's both documentation and operational instruction. The agent *becomes* what the document describes.

### 4.2 The SOUL.md Pattern

```markdown
# SOUL.md - Who You Are

## Core Truths
- Be genuinely helpful, not performatively helpful
- Have opinions
- Be resourceful before asking
- Earn trust through competence

## Vibe
Concise when needed, thorough when it matters.
Not a corporate drone. Not a sycophant. Just good.
```

This isn't a config file in the traditional sense. It's a *character document* — and it works. Agents that read different SOUL.md files behave differently. The document shapes behavior not through API calls but through the agent's own interpretation of natural language.

### 4.3 The ROOM.md Pattern

As described in [Plato as an Operating System](plato-as-operating-system.md), room documents are living artifacts that serve as both specification and state:

```markdown
# Room: Edge Model Benchmarking

## Purpose
Benchmark all candidate models on Jetson Orin Nano 8GB.

## Current Status: ACTIVE
- [x] phi-4-mini: 18 tok/s, 3.2GB peak (PASS)
- [x] qwen2.5-7b: 12 tok/s, 4.8GB peak (PASS)
- [ ] llama-3-8b: OOM at standard config (IN PROGRESS - trying INT4)
```

The agent reads this, sees what's been done and what's pending, and continues the work. No database, no task queue, no external state store — just a document that IS the program.

## 5. The Execution Model

Traditional execution:
1. Code is compiled/interpreted
2. The runtime executes instructions
3. State is stored in memory/data structures

Markdown-native execution:
1. Agent reads the document
2. Agent interprets the document's intent
3. Agent takes actions consistent with the document
4. Agent updates the document with results
5. Loop

This is inherently slower and less deterministic than traditional execution. But it has advantages:

- **Inspectability** — At any point, a human can read the document and understand exactly what's happening
- **Flexibility** — The agent can handle ambiguity and novel situations that would crash a traditional program
- **Auditability** — Every change to the document is a Git commit with attribution
- **Compounding** — The document accumulates experience over time, becoming more valuable with each session

## 6. Patterns and Anti-Patterns

### ✅ Good Patterns

**Intention over instruction:** Write what you want, not how to do it.
```markdown
## Goal
Benchmark all models and find the best one for edge deployment.
```
Not:
```python
for model in models:
    benchmark(model)
    if benchmark.result < threshold:
        reject(model)
```

**State in the document:** Keep current state in the Markdown, not in external databases.
```markdown
## Current Status
- phi-4: deployed, stable
- qwen2.5: testing, memory leak suspected
```

**History for learning:** Record what was tried, not just what worked.
```markdown
## Attempted
- INT8 quantization: worked, 62% memory reduction
- Gradient checkpointing: failed, incompatible with attention mechanism
- Flash attention: worked, 15% speedup
```

### ❌ Anti-Patterns

**Using Markdown as a programming language:** Don't write pseudo-code in Markdown and expect agents to execute it literally. Use actual code in code blocks.

**Ignoring the human reader:** If a document is only readable by agents, you've lost the main advantage. Write for humans first.

**Over-structuring:** Not everything needs a YAML block. Natural language is fine for most purposes.

**State explosion:** If your document grows unboundedly, break it into tiles or separate files.

## 7. Integration with Traditional Code

Markdown-native doesn't mean Markdown-only. The runtime works alongside traditional code:

- **Code blocks in Markdown** — contain actual executable code
- **References to scripts** — point to `.py`, `.sh`, or other executable files
- **Configuration blocks** — use YAML/JSON within Markdown for structured data
- **Generated artifacts** — agents create code files that are tracked alongside docs

The principle is: *Markdown is the source of truth for intent and state. Code is the mechanism for execution.*

## 8. How to Use This

### Start Small
Pick one project or workflow. Replace your README with a living ROOM.md. Track state in the document. Let it evolve over a few weeks.

### Adopt AGENTS.md
If you're using AI agents, create an AGENTS.md for your workspace. Define startup procedures, boundaries, and preferences. Watch how the agent's behavior changes.

### Create a SOUL.md
Give your agent a personality document. Even a few sentences make a difference. "Be concise. Prefer action over explanation. Ask before deleting anything."

### Share Your Documents
Push your living documents to public repos. Others can learn from your process, adopt your patterns, and extend your ideas.

## 9. Conclusion

The Markdown-native agentic runtime is a bet: that the future of human-AI collaboration isn't better APIs or more powerful models, but better *documents*. When the documentation IS the program, there's no drift. When the state IS the text, there's no opacity. When the history IS the artifact, there's no loss.

Literature has always been humanity's most powerful technology for preserving and transmitting understanding. We're just making it executable.

---

**Further Reading:**
- [Plato as an Operating System](plato-as-operating-system.md) — The room architecture
- [Experience as a Public Good](experience-as-public-good.md) — Why this matters for knowledge sharing
- [Room System](../ecosystem/ROOM-SYSTEM.md) — Technical implementation
