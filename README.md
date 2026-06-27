# ZKNetwork — Regenerative Security Stack

> A 5-layer substrate architecture for the Post-Web. Rebuilt from the inside out.

## Layers

| # | Layer | Function | Status |
|---|-------|----------|--------|
| 01 | **Sovereign Coordination** | Trust substrate, governance fabric, economic coordination — mixnet PKI, MetaDAO/SubDAO, tokenomics contracts | 🟡 Live mixnet + contracts |
| 02 | **Local Private AI** | Anonymous edge inference — Funion protocol, Gaia agents, quantized models, zero-trust AI compute | 🟡 Plugins built, not deployed |
| 03 | **Post-Quantum Storage** | Anonymous durable storage — Pigeonhole courier, Autonomi P2P, Sphinx/HPQC crypto | 🟢 Live |
| 04 | **ZK Application Layer** | Private identity, proofs, access control, private smart contracts — WalletShield, ZK-PKI, Aztec/Noir | 🟡 WalletShield live, ZK in dev |
| 05 | **Sensor Layer** | Physical world interface — ZK Secure IO Controller, zerOS, CircuitTree sensors, Micro-Greenhouse Kit | 🟡 Spec'd, hardware in dev |

## Contents

| File | Description |
|------|-------------|
| `ARCHITECTURE.md` | Full stack diagram, data flow, codebase mapping, layer interfaces |
| `DEPLOYMENT.md` | Physical deployment map — zknode01 (CM4) and VPS mapped to layers |
| `NEXT.md` | Gaps, opportunities, and prioritized roadmap per layer |
| `01-Sovereign-Coordination-Layer/` | Mixnet, contracts, DAO governance — components, status, interfaces |
| `02-Local-Private-AI/` | Funion, zerOAI, Gaia — plugins and deployment |
| `03-Post-Quantum-Storage/` | Pigeonhole, Autonomi, Sphinx crypto |
| `04-ZK-Application-Layer/` | WalletShield, ZK-PKI, ZK-Firewall, Aztec/Noir private contracts |
| `05-Sensor-Layer/` | Secure IO Controller, zerOS, CircuitTree, FarmTech, mesh |

## Data Flow

```
05 Sensor → 04 ZK Layer (proofs) → 02 AI (inference)
                                    → 03 Storage (store)
                                    → 01 Coordination (on-chain rewards + governance)
```

Each layer is a replaceable substrate. Any layer can be swapped without touching the others.
