# What's Next — Gaps, Opportunities, and the Next Horizon

> Rebuilding from the substrate up means we can see exactly where the gaps are — and what becomes possible when we fill them.

---

## Layer 01 — Sovereign Coordination

### Gaps

| Gap | Impact |
|-----|--------|
| No on-chain SubDAO registry | SubDAOs exist in docs but not as deployable contracts — can't programmatically create or verify a SubDAO |
| No cross-chain coordination | All contracts on Ethereum mainnet — communities on L2s or other chains can't participate |
| Aztec private voting not deployed | Noir contracts written but no production proving infrastructure |
| No formal verification on contracts | Tokenomics contracts handle real value but haven't been formally verified |
| No on-chain dispute resolution | SubDAO disputes have no programmed escalation path |

### What Becomes Possible

- **Sovereign SubDAO Factory** — deploy a SubDAO as a single tx: treasury, voting, membership, mixnet node registration, all at once
- **Cross-chain Coordination** — SubDAOs on Arbitrum, Base, Optimism with ZK proof bridging via the mixnet
- **Private Governance** — Aztec private voting wired to the mixnet: vote through the mixnet, cast on Aztec, tally with Noir
- **Formal Verification Pipeline** — Certora or Foundry fuzzing for all vault and governance contracts
- **On-chain Dispute Resolution** — Escalate to arbitration circuit with ZK-verified evidence from sensor layer

---

## Layer 02 — Local Private AI

### Gaps

| Gap | Impact |
|-----|--------|
| No on-device model training | Models are static — can't adapt to local conditions without cloud retraining |
| No federated learning | Each node's data stays isolated — network can't learn from aggregate patterns |
| No proof-of-inference | No way to verify that an inference was actually performed (for PoUW rewards) |
| No quantized model pipeline | Models too large for edge deployment; no tooling to ship quantized models |
| Funion plugins not wired to live mixnet | Anonymous inference works in test but not on the live VPS mixnet |

### What Becomes Possible

- **Proof-of-Inference** — Noir circuit that proves an AI model was executed on a specific input, without revealing input or output. Enables PoUW rewards for AI compute
- **Federated Learning over Mixnet** — Nodes share gradient updates (not data) through Funion — model improves network-wide without centralizing data
- **On-device Fine-tuning** — Local LoRA adapters trained on sensor data — each greenhouse's AI model adapts to its specific microclimate
- **Quantized Model Registry** — SubDAO-governed registry of approved models with ZK-verified provenance (chain of training → quantized → deployed)
- **Anonymous LLM Chat** — Wire Funion to a local LLM on the CM4: query via mixnet, inference on-device, response via SURB — no one knows who asked what

---

## Layer 03 — Post-Quantum Storage

### Gaps

| Gap | Impact |
|-----|--------|
| No content-addressed storage | No way to reference stored data by hash (no IPFS/IPLD integration) |
| No storage proof on-chain | Can't verify that data was stored for a period (needed for PoUW storage rewards) |
| No replication SLA | No guarantee that stored data survives node churn |
| Single Autonomi node | Only one ant-node (CM4) — no redundancy |
| No encrypted file storage client | No UI for users to store/retrieve files through Pigeonhole |

### What Becomes Possible

- **Proof-of-Storage** — Noir circuit that proves a node stored a specific piece of data for a specific duration — enables PoUW storage rewards
- **Content-Addressed Pigeonhole** — Store by CID, retrieve by CID — interoperable with IPFS ecosystem
- **Storage Grid** — Multiple Autonomi nodes + Pigeonhole couriers form a resilient storage mesh — data survives any single node failure
- **Private File Drop** — Encrypted file sharing through the mixnet: "send this file to zkID:abc123" — no metadata leakage
- **Sensor Data Archive** — Long-term storage of ZK-verified sensor data for climate reporting, grant verification, and historical analysis

---

## Layer 04 — ZK Application Layer

### Gaps

| Gap | Impact |
|-----|--------|
| No zkID issuance pipeline | Private identity exists as a concept but no one can actually get a zkID |
| No ZK-Firewall deployment | Proof-based access control is designed but not implemented |
| No ZK-BOM tooling | Supply chain verification is a whitepaper, not a tool |
| No production Noir proving | Noir circuits written but no proving infrastructure deployed |
| WalletShield is single-user | Only zknode01's wallet is routed through the mixnet |

### What Becomes Possible

- **zkID Wallet** — Desktop/mobile app that issues zkID via Noir registration circuit + keys stored in platform TPM/enclave. Users claim identity without email, phone, or government ID
- **ZK-Firewall for DAO Roles** — "Prove you're a certified greenhouse operator without revealing your name" — deployed as middleware in FarmTech and Governance apps
- **ZK-BOM CLI** — `zkn-bom verify firmware.bin --signer pubkey` — verifies hardware provenance with ZK proofs. Ship with every Micro-Greenhouse Kit
- **Noir Proving as a Service** — Deploy a proving service on the VPS or CM4 — clients submit witness, get back proof. Enables mobile/light clients
- **Multi-wallet WalletShield** — Route any wallet's RPC through the mixnet — not just the CM4's zymkey wallet. Browser extension does this

---

## Layer 05 — Sensor Layer

### Gaps

| Gap | Impact |
|-----|--------|
| No physical greenhouse deployed | The flagship product exists as specs and software — no real food has been grown |
| No sensor hardware integrated | CircuitTree sensors are specified but not connected to any live node |
| Mesh networking not deployed | Reticulum is in the architecture but no mesh exists between nodes |
| zerOS not built from spec | CM4 runs standard Debian — no hardened build, no immutable rootfs |
| Only one physical node (CM4) | No multi-node deployment, no mesh, no geographic distribution |

### What Becomes Possible

- **First Micro-Greenhouse Prototype** — CM4 + CircuitTree sensors + grow system in a real greenhouse. First ZK proof of food production from actual sensor data
- **zerOS Image Build** — Yocto/Buildroot-based hardened Linux for CM4 with secure boot, immutable rootfs, tamper detection
- **Two-Node Mesh** — Deploy a second CM4 (or RPi) with Reticulum → first mesh network between ZKN nodes. Demonstrate offline governance
- **Sensor → Proof Pipeline** — Wire CircuitTree → ZK Secure IO → FarmTech → Noir proof → on-chain PoUW reward. Close the loop end-to-end
- **Community Deployment** — Deploy 3-5 Micro-Greenhouse Kits at a school or community garden → first real SubDAO with real governance decisions about real food

---

## The Next Flywheel

```
Prototype first greenhouse (05)
    ↓
Generate first ZK proof of food production (04)
    ↓
Submit proof on-chain → first PoUW reward (01)
    ↓
Use rewards to fund second kit (01)
    ↓
Second kit creates mesh network (05)
    ↓
Mesh enables Anonymous AI across nodes (02)
    ↓
AI optimizes food production → more output → more proofs (02 → 04 → 01)
    ↓
Data stored in Pigeonhole/Autonomi for climate reporting (03)
    ↓
SubDAO governs expansion with private voting (01 + 04)
    ↓
Network effect: each new node strengthens all layers
```

---

## Immediate Next Steps (Priority Order)

| # | Action | Layer | Effort |
|---|--------|-------|--------|
| 1 | Wire CircuitTree sensors to a CM4, produce first real sensor data stream | 05 | 1-2 weeks |
| 2 | Build a Noir circuit that produces a "proof of food output" from sensor data | 04 | 1-2 weeks |
| 3 | Deploy Funion plugins on the VPS mixnet | 02 | 1 week |
| 4 | Ship a quantized LLM to the CM4, wire through basic Funion query | 02 | 2 weeks |
| 5 | Deploy second node, establish Reticulum mesh | 05 | 1 week |
| 6 | Build zkID issuance wallet (desktop MVP) | 04 | 2-3 weeks |
| 7 | Deploy Aztec private voting with mixnet integration | 01 + 04 | 3-4 weeks |
| 8 | Build SubDAO factory contract | 01 | 2 weeks |
| 9 | Store first production proof in Pigeonhole + verify on-chain | 03 + 01 | 1 week |
| 10 | Build zerOS image for CM4 | 05 | 3-4 weeks |
