# 03 — Post-Quantum Storage

> ZK proofs of storage. Anonymous durable data. Cryptographic guarantees that data exists where and when you need it.

## Purpose

Storage in ZKNetwork is built around verifiability: a node can produce a ZK proof that it stored a specific piece of data for a specific duration. This enables storage-backed rewards (PoUW), content-addressed retrieval, and privacy-preserving data archives. The Pigeonhole courier protocol provides optional anonymous message storage for applications that need it.

## Components

### 3a. Autonomi P2P Network

**Path:** `opt/zknode-zerOAI/` (ant-node service)

| Component | Status | Location |
|-----------|--------|----------|
| ant-node | 🟢 Live (CM4) | `opt/zknode-zerOAI/docker-compose.yml` |
| USB storage | 🟢 Designed | `opt/zknode-zerOAI/docs/AUTONOMI_USB_STORAGE.md` |

### 3b. Pigeonhole Courier Protocol

**Path:** `zknet-labs/katzenpost/courier/`

An anonymous message storage protocol within the Echomix privacy transport. Messages stored at pseudorandom locations, retrieved via SURB replies.

| Component | Status |
|-----------|--------|
| Courier server | 🟢 Live (VPS) |
| SURB reply mechanism | 🟢 Built into transport |
| Pseudorandom storage addressing | 🟢 Built into protocol |

### 3c. Post-Quantum Cryptography

**Path:** `zknet-labs/katzenpost/`

| Algorithm | Purpose |
|-----------|---------|
| HPQC KEM | Key encapsulation for transport |
| HPQC signing | Authority signatures |
| Sphinx packet format | Onion encryption |

### 3d. BoltDB / Local Storage

**Path:** `opt/` (common package)

Local key-value storage for node configs.

---

## Interfaces

| Interface | With Layer | Mechanism |
|-----------|------------|-----------|
| Store and retrieve proofs | 04 ZK Layer | Content-addressed blob |
| Store tensors | 02 AI Layer | Anonymous storage via storage_client |
| Storage-backed PoUW | 01 Coordination Layer | ZK proof of storage → on-chain reward |
| Node config | 01 Coordination Layer | BoltDB local |

---

## Status & Next

- **Live:** Autonomi P2P, Pigeonhole courier, HPQC/Sphinx crypto
- **Gap:** No proof-of-storage circuit, no content-addressed addressing (IPFS-like), no replication SLA, single Autonomi node
- **Next:** Build proof-of-storage Noir circuit, deploy storage verification on-chain, add IPFS compatibility
