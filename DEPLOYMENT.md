# Physical Deployment — 5-Layer Mapping

## zknode01 (CM4) — 192.168.9.118

```
┌──────────────────────────────────────────────────────────────────┐
│  zknode01 — CM4 (Debian 11, 8GB RAM)                             │
│                                                                  │
│  04 — ZK STACK                                                   │   
│    └─ zkwallet CLI/TUI — tx signing via zymbit                   │
│    └─ ZK-PKI, ZK-Firewall, ZK-BOM, ZK Verification Services      │
│                                                                  │
│  02 — LOCAL PRIVATE AI                                           │
│    └─ (reserved for zerOAI engine deployment)                    │
│                                                                  │
│  03 — POST-QUANTUM STORAGE                                       │
│    └─ ant-node (:12000) — Autonomi P2P storage node              │
│                                                                  │
│  01 — SECURED INTENTION COORDINATION                             │
│    └─ kpclientd — privacy transport client link                  │
│    └─ monitor.sh — health checks every 30min                     │
│                                                                  │
│  05 — SECURE HARDWARE LAYER                                      │
│    └─ zymbit (slot 21) — HSM, hardware signing root of trust     │
│    └─ zkifc — zymbit kernel interface                            |
|    └─ Walletshield / Echomix                                     │
└──────────────────────────────────────────────────────────────────┘
```

### Services (systemd)

| Service | Layer | Port | Status |
|---------|-------|------|--------|
| `walletshield` | 04 | :9200 | running |
| `ant-node` | 03 | :12000 | running |
| `kpclientd` | 01 | tunnel | running |
| `zkifc` | 05 | — | running |


---

## Deployment Gaps by Layer

| Layer | What's Deployed | What's Missing |
|-------|----------------|----------------|
| **04 — ZK Stack** | WalletShield (CM4), http_proxy (VPS), zkwallet CLI | No Noir proving service, no zkID issuance, no ZK-Firewall, no PoUW verifier deployed |
| **02 — Local Private AI** | zerOAI Docker Compose spec, Funion plugins (built) | No AI engine deployed on CM4 or VPS, Funion not wired to live mixnet |
| **03 — Post-Quantum Storage** | Courier (VPS), Autonomi ant-node (1) | No storage redundancy, no proof-of-storage circuit, no content-addressed addressing |
| **01 — Secured Intention Coordination** | 3 dirauth, 3 mix, 1 gateway, servicenode, all EVM contracts, PKI client | SubDAO on-chain registry, PoUW verifier contract, Credo Alignment Checks not automated |
| **05 — Secure Hardware Layer** | Zymbit HSM (CM4), zkifc driver | No zerOS image, no CircuitTree sensors, no greenhouse, tamper-response not configured |
