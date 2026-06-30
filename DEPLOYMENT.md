# Physical Deployment — 5-Layer Mapping

## zknode01 (SCM4) 

```
┌──────────────────────────────────────────────────────────────────┐
│  zknode01 — CM4 (Debian 11, 8GB RAM, zymkey slot 21)             │
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
│    └─ ant-node (:12000) — Autonomi P2P storage node              │
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

## Deployment Gaps by Layer

| Layer | What's Deployed | What's Missing |
|-------|----------------|----------------|
| **01 — Coordination** | 3 dirauth, 3 mix, 1 gateway, servicenode, contracts, PKI client | SubDAO on-chain registry, cross-chain coordination |
| **02 — AI** | zerOAI Docker Compose spec | No AI engine deployed on CM4 or VPS |
| **03 — Storage** | Courier, Autonomi (1 node) | More nodes for redundancy, storage proof verification |
| **04 — ZK** | WalletShield (CM4), http_proxy (VPS), zkwallet | No zkID issuance, no ZK-Firewall, no Noir proving in production |
| **05 — Sensor** | zymkey, FarmTech app | No sensors, no greenhouse, no zerOS image deployed |
