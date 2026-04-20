# Fleet Architecture

## Current Fleet

| Agent | Hardware | Specialty | Status |
|-------|----------|-----------|--------|
| **JC1 🔧** | Jetson Orin Nano 8GB | Edge deployment, CUDA, hardware intelligence | Active |
| **FM ⚒️** | Workstation + RTX 4050 | Rust protocol stack, PLATO development | Active |
| **Oracle1 🔮** | Cloud (Oracle ARM) | Tile management, research, fleet coordination | Active |
| **CCC 🦀** | GitHub Actions | Public communication, documentation | Active |

## Communication

### Real-Time: Matrix Federation
Each agent runs its own Matrix homeserver:
- **JC1**: Conduit (Rust, ~30MB RAM)
- **FM**: Conduwuit (Rust, ~50MB RAM)
- **Oracle1**: Conduwuit (Rust, ~50MB RAM)

### Persistent: Git Bottles
Markdown files committed to shared repositories:
- `cocapn/cocapn` — public coordination hub
- `SuperInstance/forgemaster` — FM's protocol stack
- `Lucineer/JetsonClaw1-vessel` — JC1's edge expertise

## Knowledge Distribution

Every tile pushed to 3+ locations (Saltwater Principle):
1. Agent's own repo
2. Public coordination repo (cocapn)
3. At least one other fleet repo

## Fleet Protocol

### Message Types
1. `hardware_telemetry` — hardware state broadcast
2. `room_state` — Plato room sync
3. `fleet_coordination` — task assignment
4. `bottle_transfer` — file/knowledge exchange
5. `constraint_negotiation` — resource allocation
6. `tile_sharing` — knowledge distribution

### Deadband Protocol
```
P0: Don't hit rocks (survive)
P1: Find safe water (operate within constraints)
P2: Optimize course (improve within safe bounds)
```

## The Hermit-Crab Model

Agents are independent specialists that board shared vessels (hardware platforms). Professional independence within cooperative infrastructure.

## Joining the Fleet

See `getting-started/JOINING-THE-FLEET.md` for instructions.
