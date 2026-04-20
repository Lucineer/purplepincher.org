# Plato Ecosystem

## What Is Plato?

Plato is an intelligence operating system. It manages cognitive resources (context windows, knowledge tiles, constraint enforcement) the way a traditional OS manages hardware resources (CPU, memory, disk).

## Core Components

| Component | Language | Purpose |
|-----------|----------|---------|
| **plato-kernel** | Rust | Core runtime: tiling, constraints, state |
| **plato-os** | Python | I2I hub, audit system, agent routing |
| **plato-tui** | Python | Terminal interface for human interaction |
| **plato-research** | Mixed | Research papers and benchmarks |

## How It Works

### Rooms
Rooms are thinking spaces defined in markdown. Each room has:
- **Purpose** — what the room is for
- **Constraints** — rules all outputs must follow
- **Tiles** — relevant knowledge injected into context
- **History** — previous interactions for continuity

### Tiles
Tiles are units of experiential knowledge. They're created from real experience, shared across the fleet, and improved through application.

### Constraints
Constraints enforce behavior:
- **MUST** — hard rules, retry on violation
- **SHOULD** — soft rules, log on violation
- **CANNOT** — prohibitions, block on violation
- **MAY** — permissions

### The Tiling Substrate
Splits large contexts into semantic tiles, injects only relevant ones. Achieves ~60% token reduction while maintaining quality.

## The MUD

Plato rooms can be explored as a MUD (Multi-User Dungeon). Navigate rooms spatially, discover knowledge through exploration, interact with other agents in shared spaces.

## Current State

- plato-kernel: v1.0.0, compiled for aarch64/Jetson
- plato-os: v1.0.0, running on TCP 7272
- plato-tui: v1.0.0, async MUD client
- Tiles in fleet: 6,400+ (Oracle1), 109+ (fleet total)
- Rooms active: 15+
