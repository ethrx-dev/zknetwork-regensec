# ZKNetwork — Regenerative Security Stack

> A zero-knowledge substrate for the Post-Web. Privacy is not a feature — it is the foundation.

## Layers

| # | Layer | Function | Status |
|---|-------|----------|--------|
| 04 | **ZK Stack** | Noir/Aztec proving, ZK-PKI, ZK-Firewall, ZK-BOM, zkApps, PoUW circuits | 🟡 Circuits in dev, ZK tools spec'd |
| 02 | **Local Private AI** | ZK-verified edge inference, anonymous AI compute | 🟡 Plugins built, not deployed |
| 03 | **Post-Quantum Storage** | ZK proofs of storage, anonymous durable data | 🟢 Live |
| 01 | **Secured Intention Coordination** | PoUW regenerative consensus, Credo-aligned governance, intention-anchored coordination | 🟡 Contracts live, PoUW in dev |
| 05 | **Secure Hardware** | Zymbit HSM, zerOS, edge compute, sensors, physical provenance | 🟡 Hardware spec'd, zymbit live |

## Contents

| File | Description |
|------|-------------|
| `ARCHITECTURE.md` | Full stack diagram, data flow, codebase mapping, layer interfaces |
| `DEPLOYMENT.md` | Physical deployment map — zknode01 (CM4) and VPS mapped to layers |
| `NEXT.md` | Gaps, opportunities, and prioritized roadmap per layer |
| `01-Sovereign-Coordination-Layer/` | PoUW regenerative consensus, Credo-aligned governance, Secured Intention Coordination |
| `02-Local-Private-AI/` | Funion anonymous inference, Gaia agents, zerOAI engine |
| `03-Post-Quantum-Storage/` | Autonomi P2P, Pigeonhole courier, Sphinx crypto |
| `04-ZK-Application-Layer/` | Noir proving, Aztec contracts, ZK-PKI, ZK-Firewall, ZK-BOM, zkApps (ZKNFA), PoUW circuits |
| `05-Sensor-Layer/` | Zymbit HSM, zerOS, ZK Secure IO Controller, CircuitTree sensors, FarmTech |

## Data Flow

```
05 Secure Hardware → 04 ZK Stack (proofs) → 02 AI (ZK-verified inference)
                                             → 03 Storage (store)
                                             → 01 Secured Intention Coordination (PoUW rewards + governance)
```

ZK is the universal trust primitive across every layer. The Echomix mixnet is an optional privacy transport module — available for layers that need metadata protection.
