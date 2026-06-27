# ZKNetwork — Regenerative Security Stack

> A zero-knowledge substrate for the Post-Web. Privacy is not a feature — it is the foundation.

## Layers

| # | Layer | Function | Status |
|---|-------|----------|--------|
| 04 | **ZK Application** | Private identity, proofs, access control, private smart contracts | 🟡 WalletShield live, ZK in dev |
| 02 | **Local Private AI** | ZK-verified edge inference, anonymous AI compute | 🟡 Plugins built, not deployed |
| 03 | **Post-Quantum Storage** | ZK proofs of storage, anonymous durable data | 🟢 Live |
| 01 | **Sovereign Coordination** | Governance, economic coordination, on-chain trust | 🟡 Contracts live, DAO in dev |
| 05 | **Sensor Layer** | Physical world data, hardware root of trust | 🟡 Spec'd, hardware in dev |

## Contents

| File | Description |
|------|-------------|
| `ARCHITECTURE.md` | Full stack diagram, data flow, codebase mapping, layer interfaces |
| `DEPLOYMENT.md` | Physical deployment map — zknode01 (CM4) and VPS mapped to layers |
| `NEXT.md` | Gaps, opportunities, and prioritized roadmap per layer |
| `01-Sovereign-Coordination-Layer/` | DAO governance, tokenomics contracts, coordination primitives |
| `02-Local-Private-AI/` | Funion anonymous inference, Gaia agents, zerOAI engine |
| `03-Post-Quantum-Storage/` | Autonomi P2P, Pigeonhole courier, Sphinx crypto |
| `04-ZK-Application-Layer/` | ZK-PKI, ZK-Firewall, ZK-BOM, Noir/Aztec private contracts, WalletShield |
| `05-Sensor-Layer/` | ZK Secure IO Controller, zerOS, CircuitTree sensors, FarmTech |

## Data Flow

```
05 Sensor → 04 ZK Layer (proofs) → 02 AI (ZK-verified inference)
                                    → 03 Storage (store)
                                    → 01 Coordination (on-chain rewards + governance)
```

ZK is the universal trust primitive across every layer. The Echomix mixnet is an optional privacy transport module — available for layers that need metadata protection, not a substrate requirement.
