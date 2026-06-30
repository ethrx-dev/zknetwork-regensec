# 04 — ZK Stack

> The programmable zero-knowledge layer. Aztec/Noir proving, private identity, access control, supply chain verification, and zkApps — all built on ZK.

## Purpose

This is the programmable ZK substrate of the stack. It provides the tooling, frameworks, and services for writing, proving, and verifying zero-knowledge circuits. Developers build on this layer using Noir and Aztec. Applications use ZK-PKI for private identity, ZK-Firewall for proof-based access control, ZK-BOM for supply chain integrity, and the ZKNFA framework for rapid zkApp development.

Every proof generated on this layer flows upward to the Secured Intention Coordination layer for reward distribution, and downward from the Secure Hardware layer for data ingestion.

## Components

### 4a. Noir Proving System

**Path:** `aztec-ballot/`, `zknet-labs/templates/zkapp-template/circuits/src/`

Noir is the domain-specific language and proving system for writing ZK circuits. It is the universal proving backend for the entire stack.

| Circuit | Purpose | Status |
|---------|---------|--------|
| Private Voting | Ballot creation, secret cast, ZK tally | 🟡 In dev |
| Agent Registry | Private identity/agent registry | 🟡 In dev |
| Operations | Operational logic | 🟡 In dev |
| PoUW — Food Output | ZK proof of verifiable food production | 🟡 Template |
| PoUW — Uptime | ZK proof of node availability | 🟡 Template |
| PoUW — Data Contribution | ZK proof of sensor data provision | 🟡 Template |
| PoUW — Skill Completion | ZK proof of educational achievement | 🟡 Template |
| PoUW — Governance | ZK proof of governance participation | 🟡 Template |
| PoUW — AI Inference | ZK proof of anonymous inference execution | 🟡 In design |
| PoUW — Storage | ZK proof of data persistence | 🟡 In design |
| ZK-BOM — Firmware | ZK proof of firmware integrity | 🟡 In design |

### 4b. Aztec Private Smart Contracts

**Path:** `aztec-ballot/`

Private smart contracts on Ethereum using Noir circuits, deployed via the Aztec network.

| Contract | Purpose | Status |
|----------|---------|--------|
| Private Voting | Secret ballot with publicly verifiable ZK tally | 🟡 In dev |
| Agent Registry | Private identity and agent registration | 🟡 In dev |
| AI Inference Registry | Registration and verification of AI inference proofs | 🟡 In dev |

### 4c. ZK-PKI (Private Trust Registry)

**Path:** `ZKN-SRC/src/core/`

Privacy-preserving identity registry where trust relationships are verified without exposing identities. The foundation for zkID.

| Capability | Status |
|-----------|--------|
| zkID issuance for private identity | 🟡 Spec'd, in dev |
| zkLogin authentication | 🟡 Spec'd, in dev |
| Credential attestation | 🟡 In design |

### 4d. ZK-Firewall (Proof-Based Access Control)

**Path:** `ZKN-SRC/src/core/`

Access control that verifies credentials via ZK proofs without disclosing underlying data.

| Capability | Status |
|-----------|--------|
| Operator certification | 🟡 In design |
| DAO role permissions | 🟡 In design |
| Age-gated content verification | 🟡 In design |

### 4e. ZK-BOM (Supply Chain Verification)

**Path:** `ZKN-SRC/src/core/`

Zero-knowledge Bill of Materials for hardware and software supply chain integrity.

| Capability | Status |
|-----------|--------|
| Hardware provenance attestation | 🟡 In design |
| Firmware integrity verification | 🟡 In design |
| Sensor calibration proof | 🟡 In design |

### 4f. ZK Verification Services

| Service | Function | Status |
|---------|----------|--------|
| PoUW proof verification | Validate all 7 reward class proofs | 🟡 In dev |
| Noir proving service | Remote proof generation for light clients | 🟡 In dev |
| zkEVM compatibility | ZK-verified identity on Ethereum | 🟡 In design |

### 4g. ZKNFA Framework (zkApp SDK)

**Path:** `zknfa-framework/`

Application framework for building ZK-enabled apps — the developer interface to the ZK stack.

| Service | Purpose |
|---------|---------|
| contracts.js | Smart contract interaction |
| identity.js | ZK identity management |
| pouw.js | Proof-of-Useful-Work integration |
| rewards.js | Rewards distribution |
| mixnet.js | Optional privacy transport |

### 4h. WalletShield — Private RPC Proxy (Optional Module)

**Path:** `opt/apps/walletshield/`, `zknetwork-client-command/`

Optional transport module for Ethereum RPC privacy. Routes transactions through the Echomix mixnet for metadata protection. Available for applications that need it — not a ZK requirement.

| Component | Status |
|-----------|--------|
| WalletShield Go binary | 🟢 Live (CM4) |
| Thin client (CM4) | 🟢 Live |
| Tauri app WalletShield page | 🟢 Built |
| WS-RPC client (browser extension) | 🟢 Built |

---

## Interfaces

| Interface | With Layer | Mechanism |
|-----------|------------|-----------|
| Generate proofs from sensor data | 05 Secure Hardware | Noir circuit RPC over encrypted local bus |
| Submit proofs for rewards | 01 Secured Intention Coordination | PoUW proof → on-chain verifier |
| Request AI inference | 02 Local Private AI | Funion anonymous RPC |
| Store/retrieve proofs | 03 Post-Quantum Storage | Content-addressed blob |
| Verify identity | 01 Secured Intention Coordination | On-chain ZK-PKI verification |

---

## Status & Next

- **Live:** WalletShield (optional RPC privacy), ZKNFA framework shell, Noir circuit templates for PoUW
- **In dev:** Aztec private voting, ZK-PKI spec, PoUW verifier contract
- **Gap:** No production Noir proving service, no zkID issuance pipeline, no ZK-Firewall or ZK-BOM deployment
- **Next:** Deploy Noir proving service on edge, build zkID issuance flow, wire PoUW verifier contract, publish ZK-Firewall as DAO middleware
