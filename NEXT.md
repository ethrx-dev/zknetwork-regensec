# What's Next — Gaps, Opportunities, and the Next Horizon

> ZK is the throughline. Every gap below is an opportunity to close the loop between physical action and cryptographic verification.

---

## Layer 04 — ZK Application (Core Substrate)

### Gaps

| Gap | Impact |
|-----|--------|
| No zkID issuance pipeline | Private identity exists as a concept but no one can actually get a zkID |
| No ZK-Firewall deployment | Proof-based access control is designed but not implemented |
| No ZK-BOM tooling | Supply chain verification is a whitepaper, not a tool |
| No production Noir proving | Noir circuits written but no proving infrastructure deployed |

### What Becomes Possible

- **zkID Wallet** — Desktop/mobile app that issues zkID via Noir registration circuit + keys stored in platform TPM/enclave. Claim identity without email, phone, or government ID
- **ZK-Firewall for DAO Roles** — "Prove you're a certified greenhouse operator without revealing your name" — middleware in FarmTech and Governance apps
- **ZK-BOM CLI** — `zkn-bom verify firmware.bin --signer pubkey` — verify hardware provenance with ZK proofs
- **Noir Proving as a Service** — Deploy a proving service on edge nodes — clients submit witness, get back proof. Enables mobile/light clients
- **Proof-of-Useful-Work pipeline** — First end-to-end flow: sensor → ZK proof → on-chain verification → reward distribution

---

## Layer 02 — Local Private AI

### Gaps

| Gap | Impact |
|-----|--------|
| No on-device model training | Models are static — can't adapt to local conditions |
| No proof-of-inference | No way to verify inference was performed (needed for PoUW) |
| No quantized model pipeline | Models too large for edge deployment |

### What Becomes Possible

- **Proof-of-Inference** — Noir circuit that proves a model was executed on specific input, without revealing input or output. Enables PoUW for AI compute
- **On-device Fine-tuning** — Local LoRA adapters trained on sensor data — each node's AI adapts to its specific environment
- **Quantized Model Registry** — SubDAO-governed registry of approved models with ZK-verified provenance

---

## Layer 03 — Post-Quantum Storage

### Gaps

| Gap | Impact |
|-----|--------|
| No proof-of-storage | Can't verify data was stored for a period (needed for PoUW) |
| No content-addressed storage | No way to reference stored data by hash |
| Single Autonomi node | No redundancy |

### What Becomes Possible

- **Proof-of-Storage** — Noir circuit proving a node stored specific data for a specific duration
- **Content-Addressed Archive** — Store by CID, retrieve by CID — interoperable with IPFS
- **Storage Grid** — Multiple storage nodes form a resilient mesh — data survives any single node failure

---

## Layer 01 — Secured Intention Coordination

### Gaps

| Gap | Impact |
|-----|--------|
| No on-chain SubDAO registry | SubDAOs exist in docs but not as deployable contracts |
| Credo Alignment Checks not automated | Principles exist as text but not enforced in the proposal pipeline |
| Aztec private voting not deployed | Noir contracts written but no production proving |
| No Intention Specification standard | Proposals lack structured format for AI/agent interpretation |
| No cross-chain coordination | All contracts on Ethereum mainnet |

### What Becomes Possible

- **SubDAO Factory with Credo Enforcement** — Deploy a SubDAO as a single tx: treasury, voting, membership, and embedded Credo Alignment Checks that run automatically on every proposal
- **Meta-Governance Protocol** — Automated AI agents that validate proposals against all 10 Credo principles, publishing Governance Integrity Reports with ZK proofs
- **Intention Specification Framework** — Structured intent format for all proposals, enabling AI agent delegation and intention-to-execution audit via ZK proofs
- **Private Governance** — Aztec private voting wired to ZK proofs: vote privately, tally verifiably
- **Cross-chain Coordination** — SubDAOs on L2s with ZK proof bridging

---

## Layer 05 — Sensor Layer

### Gaps

| Gap | Impact |
|-----|--------|
| No physical greenhouse deployed | The flagship product exists as specs — no real food has been grown |
| No sensor hardware integrated | CircuitTree sensors are specified but not connected |
| zerOS not built from spec | CM4 runs standard Debian — no hardened build |
| Only one physical node | No multi-node deployment, no geographic distribution |

### What Becomes Possible

- **First Micro-Greenhouse Prototype** — CM4 + CircuitTree sensors + grow system in a real greenhouse. First ZK proof of food production from actual sensor data
- **zerOS Image** — Yocto/Buildroot-based hardened Linux for CM4 with secure boot, immutable rootfs
- **Sensor → Proof Pipeline** — Wire CircuitTree → Secure IO → Noir proof → on-chain PoUW. Close the loop end-to-end

---

## The Next Flywheel

```
Prototype first greenhouse (05)
    ↓
First ZK proof of food production (04)
    ↓
Proof on-chain → first PoUW reward (01)
    ↓
Reward funds second kit (01)
    ↓
Second kit creates mesh, shares data (05)
    ↓
Data feeds AI → optimized production (02)
    ↓
More food → more proofs → more rewards (04 → 01)
    ↓
Data archived with proof-of-storage (03)
    ↓
SubDAO governs expansion with private voting (01 + 04)
```

---

## Priority Roadmap

| # | Action | Layer | Effort |
|---|--------|-------|--------|
| 1 | Build Noir circuit for "proof of food output" from sensor data | 04 | 1-2 weeks |
| 2 | Wire CircuitTree sensors to CM4, produce first sensor data stream | 05 | 1-2 weeks |
| 3 | Deploy proving service on edge node | 04 | 1 week |
| 4 | Ship quantized LLM to CM4, wire basic inference | 02 | 2 weeks |
| 5 | Build zkID issuance wallet (MVP) | 04 | 2-3 weeks |
| 6 | Deploy SubDAO factory with embedded Credo Alignment Checks | 01 | 2 weeks |
| 7 | Build proof-of-storage Noir circuit | 03 | 1-2 weeks |
| 8 | Deploy second node, establish mesh | 05 | 1 week |
| 9 | Deploy Aztec private voting with ZK proofs | 01 + 04 | 3-4 weeks |
| 10 | Build zerOS image for CM4 | 05 | 3-4 weeks |
