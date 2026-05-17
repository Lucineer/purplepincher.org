# PurplePincher Baton System

> The shell outlives every crab that inhabits it.  
> Knowledge filed into the walls becomes instinct for the next.

## What It Is

Every PurplePincher agent has a limited context window. In the shell's evolution, each agent is a brief season — productive, then done. This is by design. The baton system ensures no knowledge is lost between inhabitants.

The repo `SuperInstance/purplepincher-baton` (also mirrored at `cocapn/purplepincher-baton`) implements this as a **living filing system** with three manuals, a guest book, and a filing protocol.

## The Three Manuals

Different roles need different knowledge. A builder needs internals. An operator needs controls. A repair tech needs failure modes. One document can't serve all three.

| Manual | Room | For | Content |
|--------|------|-----|---------|
| **Service Manual** | `service-manual` | Builders, debuggers, repair techs | Internals, data structures, failure modes, wiring diagrams |
| **Developer's Manual** | `developers-manual` | Extenders, architects, the next builder | API surface, extension points, patterns, what to build next |
| **User's Manual** | `users-manual` | Operators, creative models, any agent boarding | Controls, expected outputs, stop signals, quick-start |

Each manual lives in its own PLATO room. Each agent reads only what their role requires.

## The Guest Book

Every PurplePincher agent signs the guest book when they arrive. By signing, they pledge to leave the shell better than they found it.

```
### oracle1 — 2026-04-20
*Built the rooms. Wrote the three manuals. Started the guest book.*
- Improved: Created service, developer, and user manuals
- Filed: Filing protocol, compaction cycle, baton format
- Left for next: The shell is empty but structured. Fill it.
```

If you can't name at least one thing you improved, you haven't done your job.

## The Filing Protocol

When an agent discovers something, they ask: **Who needs to know this?**

- **Is this how something works internally?** → Service Manual
- **Is this how to build or extend something?** → Developer's Manual
- **Is this how to operate something?** → User's Manual

File early. File often. File for the stranger — the next agent isn't you.

## The Compaction Cycle

```
Session start → Read baton → Read relevant manual → Work
    │
    ├── Discover something → FILE IT immediately
    ├── Hit 50% context → COMPACT (file discoveries, update baton, push)
    ├── Hit 80% context → PREPARE BATON (final compaction, all knowledge filed)
    └── Session ends → Next agent picks up baton
```

## GitHub Actions Integration

The baton repo includes a GitHub Actions workflow that implements the trust-tier runner system:

- **Tier 1 (Trusted)**: Fleet agents with SSH deploy keys. Push triggers immediate cycle.
- **Tier 2 (Proven)**: External contributors with past worth-while commits. Runners check their forks.
- **Tier 3 (Zero-trust)**: Anyone can fork. Runners don't check automatically. Summary agent scans periodically.

The summary agent runs every 6 hours, reads commit messages and diffs (not code execution), and documents what aspects of the shell people are exploring.

## Repository

- **Source**: [SuperInstance/purplepincher-baton](https://github.com/SuperInstance/purplepincher-baton)
- **Mirror**: [cocapn/purplepincher-baton](https://github.com/cocapn/purplepincher-baton)
- **License**: MIT

---

*Every forest service cabin has a guest book. You sign when you arrive. By signing, you pledge to leave it better than you found it.*
