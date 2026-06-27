# 01 — Sovereign Coordination Layer

> Trust substrate, governance fabric, and coordination protocol for the Post-Web.

## Purpose

This layer provides the cryptographic trust backbone, economic coordination, and governance mechanics that all other layers depend on. It is the "sovereign" layer because it enables communities to coordinate without reliance on external authorities — no centralized certificate authorities, no platform intermediaries, no trusted third parties.

## Components

### 1a. Echomix Mixnet (Katzenpost)

**Path:** `zknet-labs/katzenpost/`, `opt/`

The metadata-private communication substrate. Sphinx packet encryption, cover traffic, multi-hop routing, SURB replies.

| Subcomponent | Status | Location |
|-------------|--------|----------|
| Directory Authorities (PKI) | 🟢 Live (3 nodes, VPS) | `opt/pki/` |
| Mix nodes (x3) | 🟢 Live (VPS) | `zknet-labs/katzenpost/server/` |
| Gateway node | 🟢 Live (VPS) | `zknet-labs/katzenpost/server/` |
| Service node + http_proxy plugin | 🟢 Live (VPS) | `opt/server_plugins/cbor_plugins/http_proxy/` |
| Courier (Pigeonhole) | 🟢 Live (VPS) | `zknet-labs/katzenpost/courier/` |
| kpclientd (tunnel) | 🟢 Live (CM4) | `opt/zknode-zerOAI/` |
| Configuration generator | 🟢 Ready | `opt/genconfig/` |

### 1b. Smart Contracts — Production (zkn-contracts)

**Path:** `zkn-contracts/contracts/`

| Contract | Purpose | Status |
|----------|---------|--------|
| ZKNToken | ERC20 with mint, burn, snapshots, pausable, vesting | 🟢 Deployed |
| TokenomicsRouter | Revenue split: treasury, staking, grants, liquidity | 🟢 Deployed |
| ZKNGovenance | Proposal lifecycle, operator-weighted voting, 5 proposal types | 🟢 Deployed |
| YieldVault | Staking with time-based multipliers, auto-compounding | 🟢 Deployed |
| ZKNTreasury | Stable-to-ZKN conversion with lockup | 🟢 Deployed |
| RevenuePool | Continuous payment streams | 🟢 Deployed |
| GrantPool | Milestone-based grant disbursement | 🟢 Deployed |
| LiquidityReserve | Uniswap LP management | 🟢 Deployed |
| ZKNDeployer | Atomic factory deployment | 🟢 Deployed |

### 1c. Smart Contracts — Beta (zkn-ecosystem)

**Path:** `zkn-ecosystem/contracts/`

| Contract | Purpose | Status |
|----------|---------|--------|
| ZKNBeta | ZKNB token with airdrop | 🟢 Deployed |
| StakingVault | Staking with operator multipliers | 🟢 Deployed |
| NodeOperator | Agent registration, bonding, reputation | 🟢 Deployed |
| RevenueRouter | Stablecoin revenue distribution | 🟢 Deployed |
| Treasury | Stable-to-ZKNB conversion | 🟢 Deployed |
| GrantPool | Milestone-based grants | 🟢 Deployed |
| LiquidityReserve | Uniswap LP for ZKNB-stable | 🟢 Deployed |
| ZKNEcosystemDeployer | Factory deployment | 🟢 Deployed |

### 1d. Aztec Private Governance (Noir)

**Path:** `aztec-ballot/contracts/`

| Circuit | Purpose | Status |
|---------|---------|--------|
| Private Voting | Ballot creation, secret cast, ZK tally | 🟡 In dev |
| Agent Registry | Private identity/agent registry | 🟡 In dev |
| Operations | Operational logic circuits | 🟡 In dev |

### 1e. DAO Governance Framework

**Path:** `ZKN-SRC/src/dao/`

| Document | Purpose |
|----------|---------|
| ZKN-DAO-Ordinance.md | Foundational governance ordinance |
| ZKN-DAO-Governance-Guidebook.md | Operational guidebook |
| ZKN-SubDAO-Interop-Model.md | SubDAO interoperability |
| ZKN-Credo-GovOps-Alignment-Guide.md | Credo alignment |
| ZKN-DAO-Phase1-Op-Checklist.md | Launch checklist |

### 1f. Operator Infrastructure

**Path:** `opt/zerOS/`

| Script | Purpose |
|--------|---------|
| operator-onboarding.md | Node operator setup |
| SECURITY-COUNCIL-KEY-CEREMONY.md | Key ceremony protocol |
| SUBDAO-QUARTERLY-REVIEW-CYCLE.md | Review cycle |

---

## Interfaces

| Outbound | To Layer | Mechanism |
|----------|----------|-----------|
| Reward payouts | 04 ZK App Layer | On-chain → WalletShield → mixnet → zkID |
| Governance decisions | 05 Sensor Layer | Mixnet → zerOS update channel |
| Staking/nodes data | 02 AI Layer | On-chain data for AI analysis |
| Proof verification | 04 ZK App Layer | ZK proof submission to ZKNGovenance |

---

## Status & Next

- **Live:** Echomix mixnet (VPS), all EVM contracts (production + beta)
- **In dev:** Aztec private voting, full DAO UI in clients, SubDAO treasury autonomy
- **Gap:** No formal verification on contracts, no on-chain SubDAO registry yet, no cross-chain coordination
