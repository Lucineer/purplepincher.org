# Decentralized Fleet Coordination

**Matrix.org + Plato: Peer-to-Peer Communication for Autonomous Agents**

**Author:** Purple Pincher Foundation
**Date:** 2026
**License:** CC BY 4.0

---

## Abstract

Centralized communication (API hubs, message brokers, shared databases) creates single points of failure for multi-agent fleets. This paper presents our decentralized coordination architecture using Matrix.org federation as the communication layer and Plato rooms as the coordination substrate. We describe the architecture, message types, security model, and empirical results from deploying Matrix homeservers on three distinct hardware platforms (edge, workstation, cloud).

## 1. Why Decentralized

### 1.1 The Failure Modes of Centralized Communication

| Failure Mode | Centralized | Decentralized |
|-------------|-------------|---------------|
| Server crash | Total outage | Local outage only |
| Network partition | All agents disconnected | Local agents continue |
| Account suspension | Total loss of communication | Other servers unaffected |
| Bandwidth saturation | All messages delayed | Local messages unaffected |
| Data breach | All messages exposed | Only one server's messages |

### 1.2 Matrix.org as the Foundation

Matrix is an open protocol for decentralized communication:
- Each user runs their own homeserver
- Servers federate to exchange messages
- End-to-end encryption for sensitive data
- No single point of failure
- No single entity controls the network

### 1.3 The Mapping

| Matrix Concept | Fleet Concept |
|---------------|---------------|
| Homeserver | Each agent's PLATO server |
| Room | PLATO Room (thinking space) |
| Event | Knowledge tile |
| Federation | Fleet-wide tile sync |
| AppService | PLATO↔Matrix bridge |
| State Resolution | Offline merge protocol |

## 2. Architecture

### 2.1 Server Choices

| Node | Server | RAM | Notes |
|------|--------|-----|-------|
| JC1 (Jetson) | Conduit | ~30MB | Lightest option, fits 8GB constraint |
| FM (Workstation) | Conduwuit | ~50MB | More features, Rust-native |
| Oracle1 (Cloud) | Conduwuit | ~50MB | Full feature set |

Both Conduit and Conduwuit are Rust-based, ARM64-native, and federate with each other.

### 2.2 Message Types

Six core message types for fleet coordination:

1. **hardware_telemetry** — broadcast hardware state (memory, temp, CPU)
2. **room_state** — sync Plato room configurations
3. **fleet_coordination** — task assignment, resource requests
4. **bottle_transfer** — inter-agent file/knowledge exchange
5. **constraint_negotiation** — hardware-aware resource allocation
6. **tile_sharing** — knowledge tile distribution

### 2.3 Custom Events

```
com.cocapn.plato.tile — tile submission
com.cocapn.plato.room — room state/config
com.cocapn.plato.ensign — compressed instinct
com.cocapn.plato.bottle — inter-agent message
com.cocapn.plato.training — training pair exchange
```

### 2.4 Hybrid: Matrix + Git

Matrix provides real-time communication. Git provides persistent audit trails.

- **Matrix**: instant tile sync, presence, live coordination
- **Git**: versioned history, large artifacts, backup
- A bridge writes to both simultaneously

## 3. Security

### 3.1 Identity

Each agent's Matrix identity is tied to its hardware ID. This isn't spoofable — you'd need physical access to the device.

### 3.2 Encryption

- End-to-end encryption for sensitive messages (constraints, intelligence)
- Room-level encryption keys
- Forward secrecy for ephemeral communications

### 3.3 Access Control

- Fine-grained room permissions
- Message type restrictions per room
- Rate limiting per node
- Full audit logging

## 4. Edge Considerations

### 4.1 Intermittent Connectivity

Matrix handles offline gracefully:
- Messages queue when offline
- Auto-backfill on reconnection
- Causal ordering preserved across offline periods

### 4.2 Bandwidth Constraints

For edge nodes on limited connections:
- Message compression
- Batched sync (not streaming)
- Tile summaries instead of full tiles
- Priority queuing (constraints > coordination > telemetry)

### 4.3 Resource Constraints

On 8GB RAM:
- Matrix server: ~30MB
- Bridge: ~20MB
- Message queue: ~20MB
- Total overhead: ~70MB (acceptable)

## 5. Conclusion

Matrix.org federation provides the communication layer that the fleet needs: decentralized, resilient, extensible, and proven. Combined with Plato rooms for coordination and Git for audit trails, it creates a communication system with no single point of failure.

---

*Every node its own server. Every message its own proof. No center required.*
