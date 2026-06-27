# 04 — Zero Knowledge Application Layer

> Private identity, private proofs, private transactions. The programmable privacy layer.

## Purpose

This layer translates physical-world data (from sensors) and digital actions (governance votes, transactions, credentials) into zero-knowledge proofs. It is the layer where privacy is programmed — ZK-PKI for identity, ZK-Firewall for access control, ZK-BOM for supply chains, Noir circuits for custom proofs, and WalletShield for private RPC.

## Components

### 4a. WalletShield — Private RPC Proxy

**Path:** `opt/apps/walletshield/`, `zknetwork-client-command/`

Routes Ethereum JSON-RPC through the Echomix mixnet. Every transaction, balance check, and contract interaction is metadata-private.

| Component | Status | Location |
|-----------|--------|----------|
| WalletShield Go binary | 🟢 Live (CM4) | `opt/apps/walletshield/` |
| Thin client (CM4) | 🟢 Live | `opt/zknode-zerOAI/cm4-services/Dockerfile.walletshield` |
| Tauri app WalletShield page | 🟢 Built | `zknetwork-client-command/src/pages/MixNetworkPage.jsx` |
| WS-RPC client (extension) | 🟢 Built | `zknet/apps/ext/` |

### 4b. ZK-PKI (Private Trust Registry)

**Path:** `ZKN-SRC/src/core/`

Privacy-preserving identity registry where trust relationships are verified without exposing identities.

| Capability | Status |
|-----------|--------|
| zkID issuance for private identity | 🟡 Spec'd, in dev |
| zkLogin authentication | 🟡 Spec'd, in dev |
| Credential attestation | 🟡 In design |

### 4c. ZK-Firewall (Proof-Based Access Control)

**Path:** `ZKN-SRC/src/core/`

Access control that verifies credentials via ZK proofs without disclosing underlying data.

| Capability | Status |
|-----------|--------|
| Operator certification | 🟡 In design |
| Age-gated content | 🟡 In design |
| DAO role permissions | 🟡 In design |

### 4d. ZK-BOM (Supply Chain Verification)

**Path:** `ZKN-SRC/src/core/`

Zero-knowledge Bill of Materials for hardware and software supply chain integrity.

| Capability | Status |
|-----------|--------|
| Hardware provenance | 🟡 In design |
| Firmware integrity | 🟡 In design |
| Sensor calibration verification | 🟡 In design |

### 4e. Aztec / Noir Private Smart Contracts

**Path:** `aztec-ballot/`

Private smart contracts on Ethereum using Noir circuits.

| Contract | Purpose | Status |
|----------|---------|--------|
| Private Voting | Secret ballot, ZK tally | 🟡 In dev |
| Agent Registry | Private identity registry | 🟡 In dev |
| Operations | Operational logic | 🟡 In dev |
| AI Inference Registry | Noir circuits in zknet-0AI | 🟡 In dev |

### 4f. ZK Verification Services

**Path:** Various

| Service | Function | Status |
|---------|----------|--------|
| Proof of Useful Work | Verify food, uptime, skill, governance proofs | 🟡 In dev |
| ZK Proof verification | Programmable verifier for arbitrary Noir proofs | 🟡 In dev |
| zkEVM compatibility | ZK-verified identity on Ethereum | 🟡 In design |

### 4g. ZKNFA Framework

**Path:** `zknfa-framework/`

Zero-Knowledge Non-Fungible Application framework for building ZK apps.

| Service | Purpose |
|---------|---------|
| contracts.js | Smart contract interaction |
| identity.js | Identity management |
| mixnet.js | Mixnet integration |
| pouw.js | Proof-of-Useful-Work |
| rewards.js | Rewards distribution |

---

## Interfaces

| Interface | With Layer | Mechanism |
|-----------|------------|-----------|
| Receive sensor data | 05 Sensor Layer | Encrypted CBOR over local bus |
| Submit proofs on-chain | 01 Coordination Layer | WalletShield → mixnet → Ethereum |
| Request AI inference | 02 AI Layer | Funion anonymous RPC |
| Store proofs | 03 Storage Layer | Pigeonhole SURB put |
| Verify identity | 01 Coordination Layer (PKI) | Mixnet → ZK-PKI |

---

## Status & Next

- **Live:** WalletShield (RPC privacy via mixnet), ZKNFA framework shell
- **In dev:** Aztec private voting, Noir circuits, ZK-PKI spec
- **Gap:** No working zkID issuance pipeline, no ZK-Firewall deployment, no ZK-BOM tooling, no production Noir proving infrastructure
- **Next:** Build zkID issuance flow (Noir → zkApp → zkID wallet), deploy ZK-Firewall for DAO roles, integrate Noir proving into PoUW pipeline
