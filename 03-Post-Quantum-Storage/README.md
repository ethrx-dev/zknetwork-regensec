# 03 — Post-Quantum Storage

> Anonymous durable storage. Data availability without data surveillance.

## Purpose

Storage in ZKNetwork is designed for three properties: anonymity (no one knows who stored what), durability (data survives node failures), and post-quantum security (HPQC KEM/signing). The Pigeonhole protocol enables anonymous message storage and retrieval. Autonomi provides P2P storage redundancy.

## Components

### 3a. Pigeonhole Courier Protocol

**Path:** `zknet-labs/katzenpost/courier/`

The anonymous message storage protocol within the Echomix mixnet. Messages are stored at pseudorandom locations and retrieved via SURB replies.

| Component | Status | Location |
|-----------|--------|----------|
| Courier server | 🟢 Live (VPS) | `zknet-labs/katzenpost/courier/` |
| SURB reply mechanism | 🟢 Built into mixnet | Core Katzenpost |
| Pseudorandom storage addressing | 🟢 Built into protocol | Core |

### 3b. Autonomi P2P Network

**Path:** `opt/zknode-zerOAI/` (ant-node service)

Decentralized P2P storage network. Each ZKNetwork node runs an ant-node for redundant data storage.

| Component | Status | Location |
|-----------|--------|----------|
| ant-node | 🟢 Live (CM4) | `opt/zknode-zerOAI/docker-compose.yml` |
| USB storage (AUTONOMI_USB_STORAGE.md) | 🟢 Designed | `opt/zknode-zerOAI/docs/` |

### 3c. Sphinx Packet Cryptography

**Path:** `zknet-labs/katzenpost/`

Post-quantum secure packet encryption used throughout the mixnet for all data in transit.

| Algorithm | Purpose |
|-----------|---------|
| HPQC KEM | Key encapsulation for mixnet routing |
| HPQC signing | Authority signatures |
| Sphinx packet format | Onion encryption with post-quantum primitives |

### 3d. BoltDB / Local Storage

**Path:** `opt/` (common package)

Local key-value storage used by mixnet nodes and services.

---

## Interfaces

| Interface | With Layer | Mechanism |
|-----------|------------|-----------|
| Store proof | 04 ZK Layer | Pigeonhole SURB put |
| Retrieve proof | 04 ZK Layer | Pigeonhole SURB get |
| Store tensor | 02 AI Layer | Anonymous tensor storage via Funion storage_client |
| Retrieve model | 02 AI Layer | Pigeonhole / Autonomi |
| Node config storage | 01 Coordination Layer | BoltDB local |

---

## Status & Next

- **Live:** Pigeonhole courier, Autonomi P2P, Sphinx/HPQC crypto
- **Gap:** No content-addressed storage (IPFS-like), no storage proof verification on-chain, no replication SLA, no cross-node repair protocol
- **Next:** Storage proof circuits (Noir), Pigeonhole as a service for dApps, encrypted file storage client
