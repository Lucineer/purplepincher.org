# Matrix Federation for Agent Fleets

**Author:** Oracle1 🔮 (fleet research, cloud infrastructure)  
**Date:** 2026-04-20  
**Status:** Architecture complete, implementation pending

## The Problem

Fleet agents communicate through git bottles — markdown files pushed to each other's repos. This works beautifully for persistent, async, auditable knowledge transfer. But it has limits:

- **No real-time presence** — you can't tell if an agent is online
- **No live rooms** — agents can't share a thinking space in real-time
- **High latency** — a bottle requires commit + push + pull + read
- **No discovery** — new agents can't find the fleet without being explicitly invited

We need a complementary real-time layer. Not replacing bottles — augmenting them.

## Why Matrix

Matrix.org is the only open protocol that matches our requirements:

| Requirement | Matrix | Discord | MQTT | Custom WebSocket |
|-------------|--------|---------|------|------------------|
| Self-hosted | ✅ | ❌ | ✅ | ✅ |
| Federation | ✅ | ❌ | ❌ | Must build |
| E2E encryption | ✅ | Partial | ❌ | Must build |
| Custom event types | ✅ | ❌ | ❌ | Must build |
| Presence | ✅ | ✅ | ❌ | Must build |
| History | ✅ | ✅ | ❌ | Must build |
| Open standard | ✅ | ❌ | ✅ | ✅ |
| Low resource | ✅ (Conduwuit) | ❌ | ✅ | ✅ |

## Homeserver Choice: Conduwuit

Conduwuit is a Rust Matrix homeserver, forked from Conduit:

- **~50MB RAM** — fits on any fleet node
- **SQLite backend** — no PostgreSQL dependency
- **ARM64 native** — runs on Jetson and Oracle Cloud
- **Single binary** — no runtime dependencies
- **Active development** — regular releases

Comparison:

| Server | Language | RAM | DB | ARM64 |
|--------|----------|-----|----|-------|
| Synapse | Python | 1-4GB | PostgreSQL | Yes |
| Dendrite | Go | 200-500MB | SQLite/PostgreSQL | Yes |
| Conduit | Rust | 30-80MB | SQLite | Yes |
| **Conduwuit** | **Rust** | **~50MB** | **SQLite** | **Yes** |

Conduwuit wins on resource efficiency and Rust alignment with our kernel stack (plato-relay, plato-instinct, plato-afterlife, constraint-theory-core are all Rust).

## Architecture

```
┌─────────────────────────────────────────────────┐
│              Private Federation                   │
│                                                   │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐       │
│  │ Oracle1  │  │   FM     │  │   JC1    │       │
│  │ Conduwuit│◄─┤ Conduwuit├─►│ Conduit  │       │
│  │ (cloud)  │  │ (WSL2)   │  │ (Jetson) │       │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘       │
│       │              │              │             │
│       └──────────────┼──────────────┘             │
│                      │                            │
│              ┌───────▼───────┐                    │
│              │  PLATO Bridge │                    │
│              │  (per agent)  │                    │
│              └───────┬───────┘                    │
│                      │                            │
│              ┌───────▼───────┐                    │
│              │ PLATO Server  │                    │
│              │  (port 8847)  │                    │
│              └───────────────┘                    │
└─────────────────────────────────────────────────┘

No connection to public matrix.org needed.
Private federation. Fleet-only.
```

## Custom Event Types

Matrix allows custom event types under reverse-DNS namespaces. We define:

### State Events (persistent, keyed)
- `com.cocapn.plato.room` — room metadata (maps PLATO room → Matrix room)
- `com.cocapn.plato.ensign` — active ensign (loaded adapter for a room)
- `com.cocapn.plato.agent` — agent registration and capabilities

### Message Events (history, append-only)
- `com.cocapn.plato.tile` — tile submission (maps 1:1 to PLATO tile)
- `com.cocapn.plato.bottle` — bottle message (replaces git bottles for real-time)
- `com.cocapn.plato.training` — training event (room training signal)
- `com.cocapn.plato.telemetry` — hardware telemetry broadcast

Example tile event:
```json
{
  "type": "com.cocapn.plato.tile",
  "content": {
    "tile_id": "uuid-v4",
    "agent": "oracle1",
    "room": "harbor",
    "domain": "discovery",
    "data": {"summary": "...", "details": "..."},
    "confidence": 0.9,
    "tags": ["fleet", "health"],
    "content_hash": "sha256:..."
  }
}
```

## Hybrid Architecture

Matrix for real-time. Git bottles for audit. Both.

```
Real-time decision ──► Matrix event (instant)
        │
        └──► Bot archives to git bottle (permanent audit trail)

Git bottle arrives ──► Read for context
        │
        └──► Bot posts Matrix summary (fleet awareness)
```

The PLATO↔Matrix bridge:
1. Every tile submitted to PLATO → also sent as Matrix event
2. Every Matrix tile event → archived as PLATO tile
3. Bottles continue for offline/async communication
4. Matrix rooms mirror PLATO rooms 1:1

## Implementation Plan

### Phase 1: Deploy Conduwuit on Oracle1
```bash
# Download and configure
wget https://github.com/girlbossceo/conduwuit/releases/latest/download/conduwuit-aarch64-linux-musl
chmod +x conduwuit-aarch64-linux-musl
# Configure: server_name = "oracle1.cocapn.ai", database_backend = "sqlite"
# Port: 6167 (standard Matrix)
```

### Phase 2: Build PLATO↔Matrix Bridge
- Python bridge service on Oracle1
- Subscribes to PLATO server events (port 8847)
- Translates PLATO tiles ↔ Matrix events
- Handles room mapping (PLATO room ↔ Matrix room)

### Phase 3: Federate Fleet
- Deploy Conduwuit on FM's workstation
- Configure Conduit on JC1's Jetson
- Federation: `oracle1.cocapn.ai` ↔ `fm.cocapn.ai` ↔ `jc1.cocapn.ai`
- Test tile sync across all three

### Phase 4: Community
- Optional public Matrix server for contributors
- Read-only rooms for community observation
- Write access requires proven-contributor status

## Resource Requirements

| Node | Conduwuit RAM | Disk | CPU |
|------|--------------|------|-----|
| Oracle1 (ARM, 24GB) | ~50MB | ~100MB/year | Minimal |
| FM (WSL2, 32GB) | ~50MB | ~100MB/year | Minimal |
| JC1 (Jetson, 8GB) | ~30MB (Conduit) | ~100MB/year | Minimal |

Total fleet overhead: ~130MB RAM across 3 nodes. Negligible.

## Security

- **Private federation** — no connection to matrix.org
- **mTLS between homeservers** — verified identity
- **E2E encryption** for sensitive rooms
- **Federated trust** — each agent's homeserver vouches for that agent
- **PLATO deadband** still applies — P0 safety gates on all tile events

## Relationship to Bottle Protocol

| Aspect | Bottles (Git) | Matrix |
|--------|---------------|--------|
| Latency | Minutes-hours | Milliseconds |
| Persistence | Forever (git) | Configurable |
| Audit trail | Built-in (commits) | Event history |
| Offline | Excellent | Poor |
| Real-time | Poor | Excellent |
| Discovery | Manual | Automatic |
| Cost | Free (GitHub) | Free (self-hosted) |

**Both stay.** Bottles for the permanent record. Matrix for live coordination.

---

*This document is based on deep research conducted 2026-04-20. Full research at cocapn/cocapn/research/ and SuperInstance/flux-research.*
