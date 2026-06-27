# Physical Deployment — 5-Layer Mapping

## zknode01 (CM4) — 192.168.9.118

```
┌──────────────────────────────────────────────────────────────────┐
│  zknode01 — CM4 (Debian 11, 8GB RAM, zymkey slot 21)            │
│                                                                  │
│  05 — SENSOR LAYER                                               │
│    └─ zymkey (slot 21) — hardware signing root of trust          │
│                                                                  │
│  04 — ZK APPLICATION LAYER                                       │
│    └─ walletshield — optional RPC privacy proxy (:9200)          │
│    └─ zkwallet CLI/TUI — transaction signing via zymkey          │
│    └─ monitor.sh — health checks every 30min                     │
│                                                                  │
│  03 — POST-QUANTUM STORAGE                                       │
│    └─ ant-node (:12000) — Autonomi P2P storage node             │
│                                                                  │
│  02 — LOCAL PRIVATE AI                                           │
│    └─ (reserved for future zerOAI engine deployment)             │
│                                                                  │
│  01 — SOVEREIGN COORDINATION LAYER                               │
│    └─ kpclientd — privacy transport client link                  │
│    └─ monitor.sh — health checks                                 │
└──────────────────────────────────────────────────────────────────┘
```

### Services (systemd)

| Service | Layer | Port | Status |
|---------|-------|------|--------|
| `walletshield` | 04 | :9200 | running |
| `ant-node` | 03 | :12000 | running |
| `zkifc` | 05 | — | running |
| `kpclientd` | 01 | tunnel | running |

---

## VPS — 217.60.7.200

```
┌──────────────────────────────────────────────────────────────────┐
│  VPS (Debian 12, 8GB RAM, 76GB disk)                            │
│                                                                  │
│  01 — SOVEREIGN COORDINATION LAYER                               │
│    ├─ dirauth (x3) — PKI directory authorities                  │
│    ├─ mix nodes (x3), gateway, servicenode                       │
│    └─ courier — message storage                                  │
│                                                                  │
│  04 — ZK APPLICATION LAYER                                       │
│    └─ http_proxy plugin (managed by servicenode)                 │
│       ├─ /ethereum → ethereum-rpc.publicnode.com                │
│       ├─ /arbitrum → arb1.arbitrum.io/rpc                       │
│       ├─ /base → base-rpc.publicnode.com                        │
│       ├─ /bsc → bsc-rpc.publicnode.com                          │
│       ├─ /solana → solana-rpc.publicnode.com                    │
│       └─ /bitcoin → bitcoin-rpc.publicnode.com                  │
│                                                                  │
│  SUPPORTING INFRASTRUCTURE                                       │
│    └─ kpclientd_fixed — PKI client                               │
└──────────────────────────────────────────────────────────────────┘
```

---

## Deployment Gaps by Layer

| Layer | What's Deployed | What's Missing |
|-------|----------------|----------------|
| **04 — ZK** | WalletShield (CM4), http_proxy (VPS), zkwallet | No zkID issuance, no ZK-Firewall, no Noir proving in production |
| **01 — Coordination** | 3 dirauth, 3 mix, 1 gateway, servicenode, contracts, PKI client | SubDAO on-chain registry, cross-chain coordination |
| **03 — Storage** | Courier, Autonomi (1 node) | More nodes for redundancy, storage proof verification |
| **02 — AI** | zerOAI Docker Compose spec | No AI engine deployed on CM4 or VPS |
| **05 — Sensor** | zymkey, FarmTech app | No sensors, no greenhouse, no zerOS image deployed |
