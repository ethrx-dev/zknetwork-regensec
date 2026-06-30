# ZKNetwork — Architecture

> A zero-knowledge substrate for the Post-Web. Privacy is not a feature — it is the foundation.

## Stack

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
│  │   ZK-PKI  │  ZK-Firewall  │  ZK-BOM  │  Noir Circuits     │   │
│  │   zkID  │  Private Smart Contracts  │  ZK Verification    │   │
│  │   ─────────────────────────────────────────────────────   │   │
│  │   WalletShield (optional RPC privacy via Echomix)         │   │
│  └───────────────────────────────────────────────────────────┘   │
│                           │                                      │
│  ┌────────────────────────▼──────────────────────────────────┐   │
│  │                  02 — LOCAL PRIVATE AI                    │   │
│  │   ZK-Verified Inference  │  Funion Anonymous RPC          │   │
│  │   Gaia Edge Agents  │  Quantized Models  │  zerOAI Engine │   │
│  │   ─────────────────────────────────────────────────────   │   │
│  │   Optional: Echnomix / Pigeonhole for query unlinkability │   │
│  └────────────────────────┬──────────────────────────────────┘   │
│                           │                                      │
│  ┌────────────────────────▼──────────────────────────────────┐   │
│  │                  03 — POST-QUANTUM STORAGE                │   │
│  │   ZK Proofs of Storage  │  Autonomi P2P  │  Pigeonhole    │   │
│  │   Content-Addressed Archive  │  Encrypted Blob Store      │   │
│  │   ─────────────────────────────────────────────────────   │   │
│  │   Optional: mixnet SURB for anonymous storage ops         │   │
│  └────────────────────────┬──────────────────────────────────┘   │
│                           │                                      │
│  ┌────────────────────────▼──────────────────────────────────┐   │
│  │                  01 — SOVEREIGN COORDINATION LAYER        │   │
│  │   MetaDAO / SubDAO  │  TokenomicsRouter  │  ZKNGovenance  │   │
│  │   Staking Vaults  │  Revenue Pools  │  Grant Disbursement │   │
│  │   ─────────────────────────────────────────────────────   │   │
│  │   Echomix nodes (optional privacy transport substrate)    │   │
│  └────────────────────────┬──────────────────────────────────┘   │
│                           │                                      │
│  ┌────────────────────────▼──────────────────────────────────┐   │
│  │                  05 — SENSOR LAYER                        │   │
│  │ ZK Secure IO Controller  │  zerOS  │  CircuitTree Sensors │   │
│  │   Micro-Greenhouse Kit  │  Mesh Transport  │  FarmTech    │   │
│  └───────────────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────────────┘
```

---

## Layer Map

| Layer | Function | Key Components | Status |
|-------|----------|----------------|--------|
| **04 — ZK Application** | Private identity, proofs, access control, smart contracts | ZK-PKI, ZK-Firewall, ZK-BOM, Noir circuits, Aztec private contracts, WalletShield | 🟡 WalletShield live; ZK services in dev |
| **02 — Local Private AI** | ZK-verified edge inference, anonymous AI | Funion protocol, Gaia agents, zerOAI engine, quantized models | 🟡 Plugins built; not yet deployed |
| **03 — Post-Quantum Storage** | ZK proofs of storage, anonymous durable storage | Autonomi P2P, Pigeonhole courier, Sphinx/HPQC crypto | 🟢 Live |
| **01 — Sovereign Coordination** | Governance, economic coordination, trust substrate | MetaDAO/SubDAO contracts, TokenomicsRouter, ZKNGovenance, vaults, Echomix PKI | 🟡 Contracts live; DAO in dev |
| **05 — Sensor Layer** | Physical world data, hardware root of trust | ZK Secure IO Controller, zerOS, CircuitTree sensors, Micro-Greenhouse Kit, FarmTech | 🟡 Hardware spec'd; FarmTech built |

---

## Data Flow

```
05 Sensor → 04 ZK Layer (proofs generated from sensor data)
                │
                ├─→ 02 AI (ZK-verified inference)
                ├─→ 03 Storage (proofs + data stored on-chain and off-chain)
                └─→ 01 Coordination (rewards distributed, governance enacted)
```

No layer depends on the mixnet. Each layer uses ZK as its trust primitive. The mixnet (Echomix) is an optional transport module available to any layer that needs metadata privacy — WalletShield, Funion, or Pigeonhole — but it is not a substrate requirement.

---

## Codebase Mapping

| Layer | Directories |
|-------|-------------|
| **04 — ZK Layer** | `aztec-ballot/` (Noir contracts), `opt/apps/walletshield/` (RPC privacy), `zknfa-framework/` (ZK app framework), `ZKN-SRC/src/core/` (ZK-PKI, ZK-Firewall specs), `zknetwork-client-command/` (WalletShield UI) |
| **02 — AI** | `opt/zknode-zerOAI/` (zerOAI engine), `zknet-0AI/opt/server_plugins/ai_inference/` (Funion plugins), `zknet-farmtech/` (Gaia AI page) |
| **03 — Storage** | `zknet-labs/katzenpost/courier/` (Pigeonhole), `opt/zknode-zerOAI/` (ant-node), `opt/` (BoltDB) |
| **01 — Coordination** | `zkn-contracts/` (governance, tokenomics, vaults), `zkn-ecosystem/` (beta contracts), `opt/pki/` (authority server), `opt/genconfig/`, `ZKN-SRC/src/dao/` (governance docs) |
| **05 — Sensor** | `zknet-farmtech/` (FarmTech app), `ZerOSv2/` (OS spec), `ZKN-SRC/src/ops/` (Micro-Greenhouse specs) |

---

## Key Interfaces

| Interface | From | To | Protocol |
|-----------|------|----|----------|
| Sensor data ingestion | 05 Sensor | 04 ZK Layer | Encrypted CBOR over local bus |
| ZK proof generation | 05 Sensor | 04 ZK Layer | Noir circuit RPC |
| Proof submission | 04 ZK Layer | 01 Coordination | On-chain (optionally via WalletShield) |
| AI inference request | 05 Sensor | 02 AI | Funion anonymous RPC |
| Storage put/get | 04 ZK Layer | 03 Storage | Content-addressed blob |
| Governance vote | 04 ZK Layer (zkID) | 01 Coordination | On-chain (optionally via Aztec private contract) |
| Reward distribution | 01 Coordination | 04 ZK Layer (zkID) | On-chain |
| Configuration | 01 Coordination (SubDAO) | 05 Sensor | Encrypted channel → zerOS |
