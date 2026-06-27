# Physical Deployment — 5-Layer Mapping

## zknode01 (CM4) — 192.168.9.118

```
┌──────────────────────────────────────────────────────────────────┐
│  zknode01 — CM4 (Debian 11, 8GB RAM, zymkey slot 21)             │
│                                                                  │
│  05 — SENSOR LAYER                                               │
│    └─ zymkey (slot 21) — hardware signing root of trust          │
│                                                                  │
│  04 — ZK APPLICATION LAYER                                       │
│    └─ walletshield (thin client, :9200) — RPC privacy proxy      │
│                                                                  │
│  03 — POST-QUANTUM STORAGE                                       │
│    └─ ant-node (:12000) — Autonomi P2P storage node              │
│                                                                  │
│  02 — LOCAL PRIVATE AI                                           │
│    └─ (reserved for future zerOAI engine deployment)             │
│                                                                  │
│  01 — SOVEREIGN COORDINATION LAYER                               │
│    └─ kpclientd-tunnel (SSH :64331 → VPS) — mixnet client link   │
│    └─ zkwallet CLI/TUI — transaction signing via zymkey          │
│    └─ monitor.sh — health checks every 30min                     │
└──────────────────────────────────────────────────────────────────┘
```

### Services (systemd)

| Service | Layer | Port | Status |
|---------|-------|------|--------|
| `kpclientd-tunnel` | 01 | :64331→VPS | running |
| `walletshield` | 04 | :9200 | running |
| `ant-node` | 03 | :12000 | running |
| `zkifc` | 05 | — | running |

### Boot Chain

```
network → kpclientd-tunnel (01) → walletshield (04) → ant-node (03)
```

---

## VPS — 217.60.7.200

```
┌──────────────────────────────────────────────────────────────────┐
│  VPS (Debian 12, 8GB RAM, 76GB disk)                             │
│                                                                  │
│  01 — SOVEREIGN COORDINATION LAYER                               │
│    ├─ dirauth 1 (:30001) — PKI directory authority               │
│    ├─ dirauth 2 (:30002) — PKI directory authority               │
│    ├─ dirauth 3 (:30003) — PKI directory authority               │
│    ├─ mix1 (:5000) — mix node                                    │
│    ├─ mix2 (:5001) — mix node                                    │
│    ├─ mix3 (:5002) — mix node                                    │
│    ├─ gateway1 (:4000) — entry gateway                           │
│    ├─ servicenode1 (:30007) — exit node + http_proxy plugin      │
│    └─ courier — Pigeonhole message storage                       │
│                                                                  │
│  LAYER 04 — ZK APPLICATION LAYER                                 │
│    └─ http_proxy plugin (managed by servicenode1)                │
│       ├─ /ethereum → ethereum-rpc.publicnode.com                 │
│       ├─ /arbitrum → arb1.arbitrum.io/rpc                        │
│       ├─ /base → base-rpc.publicnode.com                         │
│       ├─ /bsc → bsc-rpc.publicnode.com                           │
│       ├─ /solana → solana-rpc.publicnode.com                     │
│       └─ /bitcoin → bitcoin-rpc.publicnode.com                   │
│                                                                  │
│  SUPPORTING INFRASTRUCTURE                                       │
│    └─ kpclientd_fixed — PKI client (patched timeout)             │
└──────────────────────────────────────────────────────────────────┘
```

### Mixnet Processes (user: ethrx-dev)

| Process | Layer | Uptime |
|---------|-------|--------|
| `dirauth` (x3) | 01 | 5 days |
| `server` (gateway1) | 01 | 5 days |
| `server` (mix1/2/3) | 01 | 5 days |
| `server` (servicenode1) | 01 | 0 days |
| `courier` | 03 | 19 days |
| `kpclientd_fixed` | 01 | ~18h |
| `http_proxy` | 04 | ~18h |

---

## Deployment Gaps by Layer

| Layer | What's Deployed | What's Missing |
|-------|----------------|----------------|
| **01** | 3 dirauth, 3 mix, 1 gateway, 1 servicenode, kpclientd, contracts | SubDAO on-chain registry, cross-chain coordination |
| **02** | zerOAI Docker Compose spec | No AI engine actually deployed on CM4 or VPS yet |
| **03** | Courier, Autonomi (1 node) | More Autonomi nodes for redundancy, storage SLA |
| **04** | WalletShield (CM4), http_proxy (VPS), zkwallet | No zkID issuance, no ZK-Firewall, no Noir proving in production |
| **05** | zymkey, FarmTech app | No sensors, no greenhouse, no zerOS image deployed |
