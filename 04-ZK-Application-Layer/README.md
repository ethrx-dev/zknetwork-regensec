# 04 — Zero Knowledge Application Layer

> The programmable privacy layer. Identity, proofs, access control, and private smart contracts — all built on ZK.

## Purpose

This is the core substrate of the stack. Every proof, every identity, every private transaction flows through this layer. ZK-PKI provides private identity. ZK-Firewall provides proof-based access control. ZK-BOM provides supply chain verification. Noir circuits provide programmable verification for any use case. WalletShield provides optional Ethereum RPC privacy via the Echomix transport.

## Components

### 4a. ZK-PKI (Private Trust Registry)

**Path:** `ZKN-SRC/src/core/`

Privacy-preserving identity registry where trust relationships are verified without exposing identities.

| Capability | Status |
|-----------|--------|
| zkID issuance for private identity | 🟡 Spec'd, in dev |
| zkLogin authentication | 🟡 Spec'd, in dev |
| Credential attestation | 🟡 In design |

### 4b. ZK-Firewall (Proof-Based Access Control)

**Path:** `ZKN-SRC/src/core/`

Access control that verifies credentials via ZK proofs without disclosing underlying data.

| Capability | Status |
|-----------|--------|
| Operator certification | 🟡 In design |
| DAO role permissions | 🟡 In design |

### 4c. ZK-BOM (Supply Chain Verification)

**Path:** `ZKN-SRC/src/core/`

Zero-knowledge Bill of Materials for hardware and software supply chain integrity.

| Capability | Status |
|-----------|--------|
| Hardware provenance | 🟡 In design |
| Firmware integrity | 🟡 In design |

### 4d. Noir / Aztec Private Smart Contracts

**Path:** `aztec-ballot/`

| Contract | Purpose | Status |
|----------|---------|--------|
| Private Voting | Secret ballot, ZK tally | 🟡 In dev |
| Agent Registry | Private identity registry | 🟡 In dev |
| Operations | Operational logic | 🟡 In dev |
| AI Inference Registry | Noir circuits for inference verification | 🟡 In dev |

### 4e. WalletShield — Private RPC Proxy (Optional Module)

**Path:** `opt/apps/walletshield/`, `zknetwork-client-command/`

Optional transport module that routes Ethereum JSON-RPC through the Echomix mixnet for metadata privacy. Not a layer requirement — available for applications that need transaction privacy.

| Component | Status |
|-----------|--------|
| WalletShield Go binary | 🟢 Live (CM4) |
| Thin client (CM4) | 🟢 Live |
| Tauri app page | 🟢 Built |
| WS-RPC client (extension) | 🟢 Built |

### 4f. ZK Verification Services

| Service | Function | Status |
|---------|----------|--------|
| Proof of Useful Work | Verify food, uptime, skill, governance proofs | 🟡 In dev |
| ZK Proof verification | Programmable verifier for arbitrary Noir proofs | 🟡 In dev |
| zkEVM compatibility | ZK-verified identity on Ethereum | 🟡 In design |

### 4g. ZKNFA Framework

**Path:** `zknfa-framework/`

Application framework for building ZK-enabled apps.

| Service | Purpose |
|---------|---------|
| contracts.js | Smart contract interaction |
| identity.js | Identity management |
| mixnet.js | Optional transport integration |
| pouw.js | Proof-of-Useful-Work |
| rewards.js | Rewards distribution |

---

## Interfaces

| Interface | With Layer | Mechanism |
|-----------|------------|-----------|
| Receive sensor data | 05 Sensor Layer | Encrypted CBOR over local bus |
| Submit proofs on-chain | 01 Coordination Layer | On-chain (optionally via WalletShield) |
| Request AI inference | 02 AI Layer | Funion anonymous RPC |
| Store proofs | 03 Storage Layer | Content-addressed blob |
| Verify identity | 01 Coordination Layer | On-chain ZK-PKI verification |

---

## Status & Next

- **Live:** WalletShield (optional RPC privacy), ZKNFA framework shell
- **In dev:** Aztec private voting, Noir circuits, ZK-PKI spec
- **Gap:** No zkID issuance pipeline, no ZK-Firewall deployment, no ZK-BOM tooling, no production Noir proving
- **Next:** Build zkID issuance flow, deploy ZK-Firewall for DAO roles, integrate Noir proving into PoUW pipeline
