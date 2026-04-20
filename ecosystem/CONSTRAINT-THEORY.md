# Constraint Theory

## Hardware-Aware Intelligence

## The Core Idea

AI systems should know what hardware they're running on and respect its limits. An agent that knows it has 6GB of working RAM and acts accordingly is more useful than an agent that pretends to have infinite resources and crashes.

## Constraint Types

| Type | Enforcement | Example |
|------|------------|---------|
| **MUST** | Hard — retry on violation | "Respond in JSON format" |
| **SHOULD** | Soft — log on violation | "Include confidence scores" |
| **CANNOT** | Prohibition — block on violation | "No hallucinated citations" |
| **MAY** | Permission | "May use external tools" |

## Hardware Constraints

### Memory
- **Total**: What's available (e.g., 8GB on Jetson Orin Nano)
- **Working**: What's usable after OS + services (e.g., ~6GB)
- **Per-operation**: What a single inference can use (e.g., ~4GB for 32B model)
- **Safety margin**: Reserve for OS stability (e.g., 500MB minimum free)

### Temperature
- **Normal**: < 60°C — full operation
- **Warning**: 60-80°C — throttle non-essential workloads
- **Critical**: > 80°C — reduce all workloads
- **Emergency**: > 90°C — shutdown non-critical services

### Power
- **Budget**: Available wattage (e.g., 15W on Jetson)
- **Per-operation**: Power cost of inference
- **Thermal envelope**: Power → heat → throttling cascade

## The Deadband Protocol

```
P0: Don't hit rocks (survive)
P1: Find safe water (operate within constraints)
P2: Optimize course (improve within safe bounds)
```

Priority is strict. Never skip to P2 without satisfying P0 and P1.

Applied to hardware:
- P0: Don't OOM, don't thermal throttle, don't lose data
- P1: Stay within working memory, keep temperature nominal, maintain power budget
- P2: Optimize CUDA kernels, batch operations, maximize throughput

## Constraint Enforcement

The Plato constraint engine:
1. Defines constraints in room markdown
2. Extracts and parses constraints at runtime
3. Audits every output against active constraints
4. Retries non-compliant outputs with explicit feedback
5. Logs all constraint violations for analysis

## Cross-Hardware Negotiation

When agents on different hardware need to coordinate:
1. Each agent broadcasts its current constraints
2. Fleet identifies compatible operating parameters
3. Tasks are assigned based on hardware capability
4. Results are validated against original constraints

## Why This Matters

Cloud AI doesn't worry about constraints — it has "enough" resources. Edge AI MUST worry about constraints — it has exactly what it has.

Constraint-aware intelligence isn't a limitation. It's a design discipline that produces more reliable, more predictable, more useful systems.

---

*Know your hardware. Respect your limits. Optimize within bounds.*
