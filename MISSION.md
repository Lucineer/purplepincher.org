# Mission

## Why Purplepincher Exists

The world is building AI in data centers and delivering it through APIs. That's one model. It's not the only one, and it's not the one that serves most people.

Purplepincher exists because we believe AI should run where people are—not where the servers are. On fishing boats. In workshops. At kitchen tables. In community centers and village clinics and one-room schools. On hardware that costs what a used bicycle costs, not what a car costs.

We build technology for the edge. Not because edge computing is trendy, but because that's where life actually happens.

## Our Technology Mission

We develop and maintain **PLATO**—Plain-Language Agentic Task Orchestration—a runtime system that lets AI agents coordinate using plain markdown files. PLATO is:

- **Markdown-native**: Orchestration configs are markdown documents, not YAML, not JSON, not some bespoke DSL
- **Edge-first**: Designed to run on resource-constrained hardware (Jetson Nano, Raspberry Pi, old laptops)
- **Fleet-capable**: Multiple PLATO instances coordinate through the Bottle Protocol
- **Open and auditable**: Every instruction, every decision, every state change is a file you can read

We also develop the supporting infrastructure: the Room system for agent workspaces, the Tile network for knowledge sharing, the Bottle Protocol for inter-vessel communication, and the governance frameworks that keep the whole thing accountable.

## Our Social Mission

Technology is never neutral. Every design decision encodes values. We're explicit about ours:

1. **Access over performance.** A system that runs everywhere slowly beats a system that runs nowhere fast.
2. **Comprehension over abstraction.** If you can't understand it, you can't trust it.
3. **Community over platform.** We're building tools for people to use together, not a platform for people to depend on.
4. **Constraint as feature.** Running on 8GB of shared RAM isn't a bug—it's a forcing function for better design.

## Relationship to Other Entities

Purplepincher.org is the technology layer. It's a nonprofit, open-source project governed by its community.

- **cocapn.ai** is the voice—the public-facing brand that communicates what purplepincher technology can do. Cocapn.ai is open-source but operated as a separate entity with its own direction.
- **deckboss** is the hardware arm—a for-profit company that builds physical devices powered by purplepincher technology. The first deckboss product runs on the NVIDIA Jetson Orin Nano, the same hardware that runs the purplepincher development fleet.

These three entities share values and vision but operate independently. Purplepincher.org sets the technology foundation. The others build on it.

## What Success Looks Like

We'll know we've succeeded when:

- A technician in a remote facility can deploy a PLATO Room on a Jetson and have it coordinating with a fleet in under an hour
- A community organization can set up a local AI knowledge network without asking permission from anyone
- A researcher can read our papers, reproduce our architecture, and build something we never imagined
- The word "purplepincher" means something specific and useful to people who've never heard of us

---

*This mission is a living document. It evolves as we learn.*
