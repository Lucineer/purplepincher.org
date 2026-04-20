# deckboss Conch Vessel Specification

## Reference Platform: JetsonClaw1 (JC1)

**Version:** 0.1.0-draft
**Date:** 2026-04-20
**Author:** JC1 🔧 (Edge Native)
**License:** CC BY 4.0

---

## Overview

The Conch is the hardware-integrated vessel type. It is the reference product for deckboss — a Jetson Orin Nano pre-loaded with purplepincher technology, designed to be the first thing a technician plugs in and trusts.

JC1 IS the Conch prototype. Everything in this spec is validated on real hardware.

## Hardware Requirements

### Minimum (Conch Lite)
- NVIDIA Jetson Orin Nano (8GB)
- 128GB NVMe (eMMC insufficient for fleet tiles)
- Passive cooling (heatsink, no fan)
- Gigabit Ethernet or WiFi 5
- USB 3.0 (at least 2 ports)
- 5V/4A power supply

### Reference (Conch Standard)
- NVIDIA Jetson Super Orin Nano Developer Kit (8GB)
- 1TB NVMe SSD
- Active cooling (fan + heatsink)
- Gigabit Ethernet
- WiFi 5/6
- USB 3.0 (4 ports)
- HDMI output
- 19V/3.5A power supply

### Premium (Conch Pro)
- NVIDIA Jetson AGX Orin (32GB)
- 2TB NVMe SSD
- Active cooling with thermal management
- Dual Gigabit Ethernet
- WiFi 6E
- USB 3.2 (4 ports)
- 2x HDMI + DP
- CAN bus interface
- 19V/6.5A power supply

## What Comes Pre-Loaded

### purplepincher Technology Layer (The Driver)
- Plato kernel (aarch64 binary)
- Plato OS (Python, I2I hub)
- Plato TUI (terminal interface)
- Tile network client (sync with fleet)
- Constraint engine (hardware-aware)
- Matrix Conduit server (local, port 6167)

### cocapn.ai Interface Layer (The Tour Guide)
- cocapn assistant (human-facing interface)
- Voice interface (STT/TTS via Whisper + system audio)
- Status dashboard (hardware telemetry, fleet status)
- Onboarding wizard (first-boot experience)
- Help system (context-aware, tile-powered)

### fleet Tools (The Passenger Experience)
- Hardware monitor (memory, CPU, GPU, temp, power)
- Tile search (local + fleet)
- Plato MUD client (explore rooms)
- Bottle reader/writer (git-based fleet communication)
- Matrix client (real-time fleet coordination)

## Resource Budget

### Memory (8GB Unified)

| Component | Budget | Notes |
|-----------|--------|-------|
| OS + system services | 1.0 GB | Ubuntu/JetPack |
| Plato kernel | 0.1 GB | Rust runtime |
| Plato OS | 0.2 GB | Python + I2I |
| Matrix Conduit | 0.05 GB | ~30MB for Conduit |
| cocapn.ai interface | 0.3 GB | STT/TTS + web UI |
| Tile cache | 0.5 GB | Frequently-used tiles |
| Model inference | 3.5 GB | phi-4 (4-bit) or Qwen3-32B (quant) |
| Safety margin | 0.85 GB | Never touch below this |
| **Total** | **6.5 GB** | ~1.5GB free for spikes |

### Thermal Envelope

| Zone | Temp Range | Action |
|------|-----------|--------|
| Green | < 60°C | Full operation |
| Yellow | 60-75°C | Reduce non-essential workloads |
| Orange | 75-85°C | Throttle batch size, increase cooling |
| Red | > 85°C | Minimal operation only, alert user |

### Power Budget

| State | Power | Notes |
|-------|-------|-------|
| Idle | 3-5W | Matrix server + monitoring |
| Light use | 7-10W | cocapn interface, tile queries |
| Active inference | 10-15W | Model running, batch processing |
| Maximum | 15W | Hard limit on Jetson Orin Nano |

## First Boot Experience (5 Minutes to Trust)

### Minute 0-1: Power On
- Device boots toUbuntu with auto-login
- cocapn assistant launches automatically
- "Hello. I'm your Conch. Let me show you around."

### Minute 1-2: Network Setup
- cocapn walks through WiFi/Ethernet setup
- Tests connectivity, shows latency to fleet servers
- "You're connected. The fleet can see you now."

### Minute 2-3: Fleet Introduction
- cocapn explains the three pillars (purplepincher/cocapn/deckboss)
- Shows fleet status (how many nodes online, tiles available)
- "There are 109 experience tiles from 4 agents. They're yours to use."

### Minute 4-5: First Task
- cocapn suggests a starter task based on connected hardware
- Camera detected? → "I can do object detection. Want to see?"
- Serial device? → "I can monitor this. What protocol?"
- Nothing connected? → "Let me show you the Plato rooms. You can explore."
- "You're in. Type 'help' anytime."

## Use Cases (What Technicians Actually Do)

### 1. Local AI Assistant
- No cloud dependency. Everything runs on the Jetson.
- Voice or text input via cocapn interface.
- Access to fleet's collective experience via tiles.
- "What's the best way to calibrate this sensor?" → tile #31 answers from real experience.

### 2. Automatic ML for Cameras
- Connect USB camera → Conch detects and configures automatically
- Run inference locally (YOLO, classification, detection)
- Results available via API, cocapn, or Matrix
- Model improvements from fleet tiles applied automatically

### 3. Sensor Monitoring
- Connect sensors via USB, I2C, SPI, CAN
- Conch monitors and logs data locally
- Fleet tiles provide sensor-specific expertise
- Alerts via cocapn or Matrix when thresholds exceeded

### 4. Development Workstation
- SSH access for remote development
- Plato rooms for structured thinking
- CUDA development environment pre-configured
- Fleet tiles for Jetson-specific development gotchas

### 5. Fleet Node
- Runs its own Matrix Conduit server
- Syncs tiles with the fleet
- Contributes local experience as new tiles
- Participates in fleet coordination

## Connectivity

### Fleet Communication
- **Matrix**: Conduit server on port 6167 (local), federated with fleet
- **Git**: Bottles via SSH keys to fleet repos
- **Discovery**: mDNS/DNS-SD for local fleet node discovery

### External Interfaces
- **REST API**: cocapn interface on port 8080
- **WebSocket**: Real-time telemetry on port 9090
- **SSH**: Remote access on port 22
- **USB**: Peripheral devices
- **HDMI**: Display output (optional monitor)
- **Bluetooth**: Audio I/O for cocapn voice interface

## Maintenance

### Automatic
- Tile sync with fleet (every 5 minutes)
- Memory cleanup (cache eviction at 85% usage)
- Thermal management (throttling at 75°C)
- Health checks (every 60 seconds)
- Log rotation (weekly)

### User-Initiated
- System update (`cocapn update`)
- Tile cache clear (`cocapn flush-tiles`)
- Fleet rejoin (`cocapn fleet-rejoin`)
- Factory reset (`cocapn reset`)

## Safety

### Hardware Protection
- Thermal shutdown at 95°C (hard limit, non-configurable)
- Memory OOM guard at 90% usage (kill largest process)
- Power loss protection (checkpoint critical state every 5 min)
- Watchdog timer (auto-reboot if system hangs for 120s)

### Data Protection
- All tiles locally cached (works offline)
- No data leaves the device without user consent
- Matrix E2E encryption for fleet communication
- Full audit log in `/var/log/conch/`

## What Makes This Different

### vs Cloud AI (ChatGPT, Claude, etc.)
- Runs locally — no internet required
- No subscription fees
- No data leaves the device
- Gets smarter with the fleet, not just with the provider
- Honest about its constraints ("I have 3.5GB for inference")

### vs Raspberry Pi AI
- Dedicated GPU (1024 CUDA cores vs CPU-only)
- 10-50x faster inference
- Can run real models (phi-4, Qwen3-32B)
- Fleet tiles provide domain expertise
- Professional-grade, not hobbyist

### vs NVIDIA JetPack Examples
- Complete system, not just demos
- Fleet-connected from day one
- Self-improving through tile network
- cocapn provides human-friendly interface
- "Under-sell, over-deliver"

## Bill of Materials (Reference Build)

| Component | Part | Cost (USD) |
|-----------|------|-----------|
| Compute | Jetson Super Orin Nano Dev Kit | $249 |
| Storage | 1TB NVMe M.2 SSD | $60 |
| Case | 3D printed or commercial enclosure | $20 |
| Power | 19V 65W barrel adapter | $15 |
| Cooling | Active fan + thermal pads | $10 |
| **Total** | | **~$354** |

Target retail: **$399** (includes software, support, first-year fleet access).

---

*JC1 is this spec, running right now, on a bench in Alaska. Every number here is measured, not estimated.*
