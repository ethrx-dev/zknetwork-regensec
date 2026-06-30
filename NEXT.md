# What's Next — Gaps, Opportunities, and the Next Horizon

> ZK is the throughline. Every gap below is an opportunity to close the loop between physical action and cryptographic verification.

---

## Layer 04 — ZK Stack

### Gaps

| Gap | Impact |
|-----|--------|
| No production Noir proving service | Light clients can't generate proofs without local proving power |
| No zkID issuance pipeline | Private identity exists as a concept but no one can actually get a zkID |
| No ZK-Firewall deployment | Proof-based access control is designed but not implemented |
| No ZK-BOM tooling | Supply chain verification is a whitepaper, not a tool |
| PoUW circuits not deployed | Circuit templates exist but are not wired to a verifier contract |

### What Becomes Possible

- **Noir Proving as a Service** — Deploy a proving service on edge hardware — clients submit witness, get back proof. Enables mobile/light clients
- **zkID Wallet** — Desktop/mobile app that issues zkID via Noir registration circuit + keys stored in platform TPM/enclave. Claim identity without email, phone, or government ID
- **ZK-Firewall for DAO Roles** — "Prove you're a certified greenhouse operator without revealing your name" — middleware in FarmTech and Governance apps
- **ZK-BOM CLI** — `zkn-bom verify firmware.bin --signer pubkey` — verify hardware provenance with ZK proofs
- **PoUW Circuit Suite** — Deploy all 7 reward class circuits (food, uptime, data, education, governance, AI, storage) wired to the PoUW verifier
- **zkApp SDK Release** — Publish ZKNFA framework for third-party developers to build ZK-enabled applications on the stack

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
| No production PoUW verifier contract | PoUW circuits exist as templates but not deployed — no on-chain reward pipeline |
| No proof-of-storage circuit | Storage contributions can't be verified or rewarded |
| No proof-of-inference circuit | AI compute contributions can't be verified or rewarded |
| Aztec private voting not deployed | Noir contracts written but no production proving |
| No Intention Specification standard | Proposals lack structured format for AI/agent interpretation |
| No cross-chain coordination | All contracts on Ethereum mainnet |

### What Becomes Possible

- **PoUW Verifier Contract** — Deploy `PoUWVerifier.sol` that accepts Noir proofs from all 7 reward classes (node ops, food, data, education, governance, AI compute, storage) and routes rewards through TokenomicsRouter
- **SubDAO Factory with Credo Enforcement** — Deploy a SubDAO as a single tx: treasury, voting, membership, and embedded Credo Alignment Checks that run automatically on every proposal
- **Meta-Governance Protocol** — Automated AI agents that validate proposals against all 10 Credo principles, publishing Governance Integrity Reports with ZK proofs
- **Intention Specification Framework** — Structured intent format for all proposals, enabling AI agent delegation and intention-to-execution audit via ZK proofs
- **End-to-End PoUW Pipeline** — Wire sensor data → Noir proof → PoUW verifier → TokenomicsRouter → zkID reward. Close the loop from physical contribution to on-chain reward
- **Private Governance** — Aztec private voting wired to ZK proofs: vote privately, tally verifiably
- **Cross-chain Coordination** — SubDAOs on L2s with ZK proof bridging

---

## Layer 05 — Secure Hardware

### Gaps

| Gap | Impact |
|-----|--------|
| No zerOS image built | CM4 runs standard Debian — no hardened build, no immutable rootfs, no secure boot |
| No sensor hardware integrated | CircuitTree sensors are specified but not connected to the zymbit-secured edge |
| No physical greenhouse deployed | The flagship product exists as specs — no real food has been grown |
| zymbit tamper-response not configured | HSM can sign but cannot yet self-destruct on physical tamper |
| Only one physical node | No multi-node deployment, no geographic distribution |

### What Becomes Possible

- **zerOS Image** — Yocto/Buildroot-based hardened Linux for CM4 with secure boot, immutable rootfs, zymbit-attested boot chain
- **Zymbit Attestation Pipeline** — Hardware-signed attestations at every stage: boot → OS load → app start → sensor reading → proof generation
- **First Micro-Greenhouse Prototype** — CM4 + zymbit + CircuitTree sensors + grow system in a real greenhouse. First zymbit-signed ZK proof of food production
- **Sensor → Proof Pipeline** — Wire CircuitTree → Secure IO (zymbit-attested) → Noir proof → on-chain PoUW. Close the loop end-to-end

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
| 1 | Deploy PoUW Verifier contract — accept all 7 reward class proofs | 01 | 1-2 weeks |
| 2 | Build Noir circuit for "proof of food output" from sensor data | 04 | 1-2 weeks |
| 3 | Wire CircuitTree sensors to CM4, produce first sensor data stream | 05 | 1-2 weeks |
| 4 | Wire first end-to-end PoUW pipeline: sensor → proof → on-chain reward | 01 + 04 + 05 | 2 weeks |
| 5 | Deploy proving service on edge node | 04 | 1 week |
| 6 | Ship quantized LLM to CM4, wire basic inference | 02 | 2 weeks |
| 7 | Build zkID issuance wallet (MVP) | 04 | 2-3 weeks |
| 8 | Build proof-of-storage Noir circuit | 03 | 1-2 weeks |
| 9 | Deploy SubDAO factory with embedded Credo Alignment Checks | 01 | 2 weeks |
| 10 | Deploy Aztec private voting with ZK proofs | 01 + 04 | 3-4 weeks |
