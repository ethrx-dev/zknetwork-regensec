# ZKNetwork — Architecture

> The Post-Web stack rebuilt from substrate layers up.

```
┌──────────────────────────────────────────────────────────────────┐
│                        USER APPLICATIONS                         │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────────┐     │
│  │ Desktop  │ │ Browser  │ │   CLI    │ │    FarmTech      │     │
│  │ (Tauri)  │ │ (WXT)    │ │ (Rust)   │ │    (Tauri)       │     │
│  └────┬─────┘ └────┬─────┘ └────┬─────┘ └──────┬───────────┘     │
│       │            │            │              │                 │
│  ┌────▼────────────▼────────────▼──────────────▼─────────────┐   │
│  │                  04 — ZK APPLICATION LAYER                │   │
│  │   ZK-PKI │ ZK-Firewall │ ZK-BOM │ WalletShield │ zkID     │   │
│  │   Aztec/Noir Private Contracts │ ZK Verification          │   │
│  └────────────────────────┬──────────────────────────────────┘   │
│                           │                                      │
│  ┌────────────────────────▼──────────────────────────────────┐   │
│  │                  02 — LOCAL PRIVATE AI                    │   │
│  │   Funion (Anonymous Inference) │ Gaia AI Agents           │   │
│  │   zerOAI Engine │ vLLM │ Quantized Edge Models            │   │
│  └────────────────────────┬──────────────────────────────────┘   │
│                           │                                      │
│  ┌────────────────────────▼──────────────────────────────────┐   │
│  │                  03 — POST-QUANTUM STORAGE                │   │
│  │   Pigeonhole Courier │ Autonomi P2P │ Sphinx Crypto       │   │
│  │   Anonymous Tensor Storage │ BoltDB                       │   │
│  └────────────────────────┬──────────────────────────────────┘   │
│                           │                                      │
│  ┌────────────────────────▼──────────────────────────────────┐   │
│  │                  01 — SOVEREIGN COORDINATION LAYER        │   │
│  │   MetaDAO/SubDAO │ Mixnet Directory Authorities (PKI)     │   │
│  │   TokenomicsRouter │ ZKNGovenance │ Staking Vaults        │   │
│  │   Echomix Mixnet (Sphinx packets, cover traffic, SURB)    │   │
│  └────────────────────────┬──────────────────────────────────┘   │
│                           │                                      │
│  ┌────────────────────────▼──────────────────────────────────┐   │
│  │                  05 — SENSOR LAYER                        │   │
│  │   ZK Secure IO Controller │ zerOS Hardened Linux          │   │
│  │   CircuitTree IoT Sensors │ Micro-Greenhouse Kit          │   │
│  │   Mesh Networking (Reticulum)                             │   │
│  └───────────────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────────────┘
```

---

## Layer Map

| Layer | Function | Key Components | Status |
|-------|----------|----------------|--------|
| **01 — Sovereign Coordination** | Trust, governance, coordination substrate | Echomix mixnet, PKI authorities, MetaDAO/SubDAO contracts, TokenomicsRouter, ZKNGovenance, StakingVault | 🟡 Live mixnet + contracts; DAO in active dev |
| **02 — Local Private AI** | Anonymous edge inference, local intelligence | Funion (Go plugins), Gaia AI, zerOAI engine, vLLM, latency buckets, quantized models | 🟡 Funion plugins written; edge AI in dev |
| **03 — Post-Quantum Storage** | Anonymous durable storage, data availability | Pigeonhole courier protocol, Autonomi P2P network, Sphinx packet crypto, BoltDB | 🟢 Pigeonhole + Autonomi live |
| **04 — ZK Application Layer** | Private identity, proofs, access control, private smart contracts | ZK-PKI, ZK-Firewall, ZK-BOM, Aztec/Noir private voting, WalletShield RPC proxy | 🟡 WalletShield live; ZK services in dev |
| **05 — Sensor Layer** | Physical world data, edge compute, hardware root of trust | ZK Secure IO Controller, zerOS, CircuitTree sensors, Micro-Greenhouse Kit, FarmTech app | 🟡 Hardware spec'd; FarmTech built |

---

## Data Flow Across Layers

```
Sensor Layer (05)
  ↓ encrypted sensor data
ZK Application Layer (04)
  ↓ ZK proofs generated
Local Private AI (02)
  ↓ anonymous inference results
Post-Quantum Storage (03)
  ↓ proofs + data stored
Sovereign Coordination Layer (01)
  ↓ rewards, governance, coordination
Back to Sensor Layer (hardware control, adjustments)
```

---

## Codebase Mapping

| Layer | Directories |
|-------|-------------|
| **01 — Coordination** | `zkn-contracts/` (governance, tokenomics, vaults), `zkn-ecosystem/` (beta contracts), `opt/` (PKI server, genconfig), `zknet-labs/katzenpost/` (mixnet fork), `ZKN-SRC/src/dao/` (governance docs) |
| **02 — AI** | `opt/zknode-zerOAI/` (ZeroAI engine, Docker Compose), `zknet-0AI/opt/server_plugins/ai_inference/` (Funion Go plugins), `zknet-farmtech/` (Gaia AI page) |
| **03 — Storage** | `zknet-labs/katzenpost/courier/` (Pigeonhole), `opt/zknode-zerOAI/` (ant-node), `opt/` (BoltDB) |
| **04 — ZK Layer** | `aztec-ballot/` (Noir contracts), `opt/apps/walletshield/` (WalletShield), `zknfa-framework/` (ZK app framework), `ZKN-SRC/src/core/` (ZK-PKI, ZK-Firewall specs), `zknetwork-client-command/` (WalletShield UI) |
| **05 — Sensor** | `zknet-farmtech/` (FarmTech Tauri app), `ZerOSv2/` (OS spec), `ZKN-SRC/src/ops/` (Micro-Greenhouse specs), `Micro-Greenhouse_Kit_Component_Reference.md` |

---

## Key Interfaces Between Layers

| Interface | From | To | Protocol |
|-----------|------|----|----------|
| Sensor data ingestion | 05 Sensor | 04 ZK Layer | Encrypted CBOR over local bus |
| ZK proof generation request | 05 Sensor | 04 ZK Layer | Noir circuit RPC |
| Proof submission | 04 ZK Layer | 01 Coordination | On-chain via WalletShield + mixnet |
| AI inference request | 05 Sensor | 02 AI | Funion anonymous RPC |
| Storage put/get | 04 ZK Layer | 03 Storage | Pigeonhole SURB packets |
| Governance vote | 04 ZK Layer (zkID) | 01 Coordination | Mixnet → Aztec private contract |
| Reward distribution | 01 Coordination | 04 ZK Layer (zkID) | On-chain → WalletShield → mixnet |
| Configuration | 01 Coordination (SubDAO) | 05 Sensor | Mixnet → zerOS update channel |
