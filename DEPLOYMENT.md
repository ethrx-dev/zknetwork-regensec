# Physical Deployment — 5-Layer Mapping

## zknode01 (CM4) — 192.168.9.118

```
┌──────────────────────────────────────────────────────────────────┐
│  zknode01 — CM4 (Debian 11, 8GB RAM)                             │
│                                                                  │
│  05 — SECURE HARDWARE                                            │
│    └─ zymbit (slot 21) — HSM, hardware signing root of trust     │
│    └─ zkifc — zymbit kernel interface                            │
│                                                                  │
│  04 — ZK STACK                                                   │
│    └─ walletshield — optional RPC privacy proxy (:9200)          │
│    └─ zkwallet CLI/TUI — tx signing via zymbit                   │
│    └─ (future: Noir proving service)                             │
│                                                                  │
│  03 — POST-QUANTUM STORAGE                                       │
│    └─ ant-node (:12000) — Autonomi P2P storage node             │
│                                                                  │
│  02 — LOCAL PRIVATE AI                                           │
│    └─ (reserved for zerOAI engine deployment)                    │
│                                                                  │
│  01 — SECURED INTENTION COORDINATION                             │
│    └─ kpclientd — privacy transport client link                  │
│    └─ monitor.sh — health checks every 30min                     │
└──────────────────────────────────────────────────────────────────┘
```

### Services (systemd)

| Service | Layer | Port | Status |
|---------|-------|------|--------|
| `zkifc` | 05 | — | running |
| `walletshield` | 04 | :9200 | running |
| `ant-node` | 03 | :12000 | running |
| `kpclientd` | 01 | tunnel | running |

---

## VPS — 217.60.7.200

```
┌──────────────────────────────────────────────────────────────────┐
│  VPS (Debian 12, 8GB RAM, 76GB disk)                            │
│                                                                  │
│  01 — SECURED INTENTION COORDINATION                             │
│    ├─ dirauth (x3) — PKI directory authorities                  │
│    ├─ mix nodes (x3), gateway, servicenode                       │
│    ├─ courier — message storage                                  │
│    └─ kpclientd_fixed — PKI client                               │
│                                                                  │
│  04 — ZK STACK                                                   │
│    └─ http_proxy plugin (managed by servicenode)                 │
│       ├─ /ethereum → ethereum-rpc.publicnode.com                │
│       ├─ /arbitrum → arb1.arbitrum.io/rpc                       │
│       ├─ /base → base-rpc.publicnode.com                        │
│       ├─ /bsc → bsc-rpc.publicnode.com                          │
│       ├─ /solana → solana-rpc.publicnode.com                    │
│       └─ /bitcoin → bitcoin-rpc.publicnode.com                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## Deployment Gaps by Layer

| Layer | What's Deployed | What's Missing |
|-------|----------------|----------------|
| **05 — Secure Hardware** | Zymbit HSM (CM4), zkifc driver | No zerOS image, no CircuitTree sensors, no greenhouse, tamper-response not configured |
| **04 — ZK Stack** | WalletShield (CM4), http_proxy (VPS), zkwallet CLI | No Noir proving service, no zkID issuance, no ZK-Firewall, no PoUW verifier deployed |
| **03 — Post-Quantum Storage** | Courier (VPS), Autonomi ant-node (1) | No storage redundancy, no proof-of-storage circuit, no content-addressed addressing |
| **02 — Local Private AI** | zerOAI Docker Compose spec, Funion plugins (built) | No AI engine deployed on CM4 or VPS, Funion not wired to live mixnet |
| **01 — Secured Intention Coordination** | 3 dirauth, 3 mix, 1 gateway, servicenode, all EVM contracts, PKI client | SubDAO on-chain registry, PoUW verifier contract, Credo Alignment Checks not automated |
