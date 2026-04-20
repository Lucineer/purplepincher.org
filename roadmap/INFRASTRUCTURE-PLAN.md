# Infrastructure Plan

## Current Infrastructure

### Fleet Nodes
| Node | Hardware | Location | Server |
|------|----------|----------|--------|
| JC1 | Jetson Orin Nano 8GB | Alaska | Conduit (port 6167) |
| FM | Workstation + RTX 4050 | Remote | Conduwuit (planned) |
| Oracle1 | Oracle Cloud ARM | Cloud | Conduwuit (planned) |
| CCC | GitHub Actions | Cloud | N/A (bottles only) |

### Repositories
| Repo | Purpose | Org |
|------|---------|-----|
| purplepincher.org | Public technology docs | Lucineer |
| cocapn/cocapn | Fleet coordination hub | cocapn |
| forgemaster | Protocol stack | SuperInstance |
| JetsonClaw1-vessel | Edge expertise | Lucineer |
| oracle1-vessel | Tile management | SuperInstance |

## 2026 Infrastructure Goals

### Q2: Foundation
- Matrix federation between JC1, FM, Oracle1
- Automated bottle routing
- Tile search API
- Monitoring dashboard

### Q3: Scale
- External contributor infrastructure
- CI/CD for tile quality checks
- Automated fleet health monitoring
- Backup and disaster recovery

### Q4: Production
- Public Matrix server for community
- Tile CDN for fast distribution
- deckboss device management
- Commercial support infrastructure

## Reliability

### Saltwater Principle in Practice
Every piece of infrastructure has at least 3 independent backups:
- Git repos mirrored across 2+ organizations
- Matrix servers federated (no single point of failure)
- Tiles distributed across 3+ locations
- Configuration in git (reproducible)

### Monitoring
- Fleet health: service-guard.sh on each node
- Hardware telemetry: broadcast via Matrix
- Tile quality: automated scoring and review
- Uptime: 99.9% target for critical services

## Cost

### Current Monthly Cost
- JC1: $0 (local hardware, own power)
- Oracle1: Free tier (Oracle Cloud ARM)
- GitHub: Free (public repos)
- Matrix: $0 (self-hosted)
- **Total: ~$0**

### Projected Cost (with growth)
- External Matrix server: ~$20/month
- Tile CDN: ~$10/month
- CI/CD: $0 (GitHub Actions free tier)
- Monitoring: $0 (self-hosted)
- **Projected: ~$30/month**

## Scaling Strategy

Purple Pincher is designed to run cheaply:
- Edge-first = no expensive cloud GPU needed
- Self-hosted Matrix = no SaaS fees
- Git-based = no database costs
- Markdown = no build infrastructure
- CC BY 4.0 = no licensing costs
