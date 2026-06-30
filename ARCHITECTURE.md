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
│  │                      04 — ZK STACK                        │   │
│  │   Noir Proving System  │  Aztec Private Contracts         │   │
│  │   ZK-PKI  │  ZK-Firewall  │  ZK-BOM  │  zkApps (ZKNFA)    │   │
│  │   PoUW Proof Circuits  │  ZK Verification Services        │   │
│  │   ─────────────────────────────────────────────────────   │   │
│  │   WalletShield (optional RPC privacy module)              │   │
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
│  │              01 — SECURED INTENTION COORDINATION          │   │
│  │   Proof of Useful Work (PoUW) — regenerative consensus    │   │
│  │   MetaDAO / SubDAO  │  Meta-Governance Protocol           │   │
│  │   TokenomicsRouter  │  ZKNGovenance  │  Vaults            │   │
│  │   Credo Alignment Checks  │  Intention Specification      │   │
│  │   ─────────────────────────────────────────────────────   │   │
│  │   Echomix nodes (optional privacy transport)              │   │
│  └────────────────────────┬──────────────────────────────────┘   │
│                           │                                      │
│  ┌────────────────────────▼──────────────────────────────────┐   │
│  │                 05 — SECURE HARDWARE LAYER                │   │
│  │   Zymbit HSM  │  zerOS Hardened Linux                     │   │
│  │   ZK Secure IO Controller  │  CircuitTree Sensors         │   │
│  │   Micro-Greenhouse Kit  │  FarmTech  │  Mesh Transport    │   │
│  └───────────────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────────────┘
```

---

## Layer Map

| Layer | Function | Key Components | Status |
|-------|----------|----------------|--------|
| **04 — ZK Stack** | Noir proving, private identity, access control, zkApps, supply chain verification | Noir/Aztec tooling, ZK-PKI, ZK-Firewall, ZK-BOM, ZKNFA framework, PoUW circuits | 🟡 Circuits in dev; ZK tools spec'd |
| **02 — Local Private AI** | ZK-verified edge inference, anonymous AI | Funion protocol, Gaia agents, zerOAI engine, quantized models | 🟡 Plugins built; not yet deployed |
| **03 — Post-Quantum Storage** | ZK proofs of storage, anonymous durable storage | Autonomi P2P, Pigeonhole courier, Sphinx/HPQC crypto, BoltDB | 🟢 Live |
| **01 — Secured Intention Coordination** | Verifiable collective action, PoUW regenerative consensus, Credo-aligned governance | MetaDAO/SubDAO contracts, PoUW verifier, TokenomicsRouter, ZKNGovenance, Meta-Governance Protocol, vaults | 🟡 Contracts live; PoUW in dev |
| **05 — Secure Hardware** | Hardware root of trust, secure edge runtime, physical data provenance | Zymbit HSM, zerOS, ZK Secure IO Controller, CircuitTree sensors, Micro-Greenhouse Kit | 🟡 Hardware spec'd; zymbit live |

---

## Data Flow

```
05 Secure Hardware → 04 ZK Stack (Noir proofs generated from sensor data via zymbit-signed attestations)
                         │
                         ├─→ 02 AI (ZK-verified inference)
                         ├─→ 03 Storage (proofs + data stored)
                         └─→ 01 Secured Intention Coordination (PoUW rewards, governance)
```

No layer depends on the mixnet. Each layer uses ZK as its trust primitive. The mixnet (Echomix) is an optional transport module available to any layer that needs metadata privacy — WalletShield, Funion, or Pigeonhole — but it is not a substrate requirement.

Layer 01 is governed by the **Secured Intention Coordination Protocol**: every proposal, vote, and economic signal is an intention that is cryptographically committed, ZK-verified against the Credo, and executed without intermediaries. Its economic engine is **Proof of Useful Work (PoUW)** — a regenerative consensus mechanism that rewards verifiable real-world contributions instead of extractive computation or capital concentration.

---

## Codebase Mapping

| Layer | Directories |
|-------|-------------|
| **04 — ZK Stack** | `aztec-ballot/` (Noir contracts, private voting), `zknfa-framework/` (zkApp SDK), `ZKN-SRC/src/core/` (ZK-PKI, ZK-Firewall, ZK-BOM specs), `zknet-labs/templates/zkapp-template/circuits/src/pouw.nr` (PoUW circuits), `opt/apps/walletshield/` (optional RPC privacy), `zknetwork-client-command/` (WalletShield UI) |
| **02 — AI** | `opt/zknode-zerOAI/` (zerOAI engine), `zknet-0AI/opt/server_plugins/ai_inference/` (Funion plugins), `zknet-farmtech/` (Gaia AI page) |
| **03 — Storage** | `zknet-labs/katzenpost/courier/` (Pigeonhole), `opt/zknode-zerOAI/` (ant-node), `opt/` (BoltDB) |
| **01 — Secured Intention Coordination** | `zkn-contracts/` (governance, tokenomics, vaults), `zkn-ecosystem/` (beta contracts), `opt/pki/` (authority server), `opt/genconfig/`, `ZKN-SRC/src/dao/` (governance docs, Credo alignment guide), `aztec-ballot/` (private voting circuits), `zknet-labs/templates/zkapp-template/circuits/src/pouw.nr` (PoUW circuits), `zknfa-framework/src/services/pouw.js` (PoUW engine) |
| **05 — Secure Hardware** | `ZerOSv2/` (zerOS build spec), `ZKN-SRC/src/ops/` (Micro-Greenhouse specs, Secure IO Controller), `zknet-farmtech/` (FarmTech app), `SYSTEM.md` (zknode01 deployment with zymbit), `opt/zknode-zerOAI/` (node deployment, zymbit scripts) |

---

## Key Interfaces

| Interface | From | To | Protocol |
|-----------|------|----|----------|
| Sensor data ingestion | 05 Secure Hardware | 04 ZK Stack | Encrypted CBOR over local bus |
| ZK proof generation | 05 Secure Hardware | 04 ZK Stack | Noir circuit RPC (zymbit-signed) |
| Proof submission | 04 ZK Stack | 01 Secured Intention Coordination | PoUW proof → on-chain verifier |
| AI inference request | 05 Secure Hardware | 02 AI | Funion anonymous RPC |
| Storage put/get | 04 ZK Stack | 03 Storage | Content-addressed blob |
| Governance vote | 04 ZK Stack (zkID) | 01 Coordination | On-chain (optionally via Aztec private contract) |
| Reward distribution | 01 Coordination | 04 ZK Stack (zkID) | On-chain → zkID |
| Configuration | 01 Coordination (SubDAO) | 05 Secure Hardware | Encrypted channel → zerOS update system |
