# 01 — Sovereign Coordination Layer

> Governance, economic alignment, and on-chain trust. Communities coordinate without intermediaries.

## Purpose

This layer provides the economic and governance substrate — tokenomics, voting, treasury management, and contract-based coordination. All decisions flow through ZK-verified mechanisms. The optional Echomix privacy transport is available for SubDAOs that require metadata protection during voting or communication.

## Components

### 1a. Smart Contracts — Production

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

### 1b. Smart Contracts — Beta

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

### 1c. Private Governance Circuits (Noir / Aztec)

**Path:** `aztec-ballot/contracts/`

| Circuit | Purpose | Status |
|---------|---------|--------|
| Private Voting | Ballot creation, secret cast, ZK tally | 🟡 In dev |
| Agent Registry | Private identity/agent registry | 🟡 In dev |
| Operations | Operational logic circuits | 🟡 In dev |

### 1d. DAO Governance Framework

**Path:** `ZKN-SRC/src/dao/`

| Document | Purpose |
|----------|---------|
| ZKN-DAO-Ordinance.md | Foundational governance ordinance |
| ZKN-DAO-Governance-Guidebook.md | Operational guidebook |
| ZKN-SubDAO-Interop-Model.md | SubDAO interoperability |
| ZKN-Credo-GovOps-Alignment-Guide.md | Credo alignment |
| ZKN-DAO-Phase1-Op-Checklist.md | Launch checklist |

### 1e. Privacy Transport (Optional Module)

**Path:** `opt/pki/`, `zknet-labs/katzenpost/`

The Echomix mixnet — a metadata-private communication substrate using Sphinx packet encryption. Deployed as an optional privacy layer for SubDAOs and applications that require unlinkability.

| Subcomponent | Status |
|-------------|--------|
| Directory Authorities (PKI) | 🟢 Live (3 nodes, VPS) |
| Mix nodes (x3) | 🟢 Live (VPS) |
| Gateway node | 🟢 Live (VPS) |
| Service node + http_proxy plugin | 🟢 Live (VPS) |
| Courier (Pigeonhole) | 🟢 Live (VPS) |
| Configuration generator | 🟢 Ready |

---

## Interfaces

| Outbound | To Layer | Mechanism |
|----------|----------|-----------|
| Reward payouts | 04 ZK Layer | On-chain → zkID |
| Governance decisions | 05 Sensor Layer | Encrypted channel → zerOS |
| Proof verification | 04 ZK Layer | ZK proof submission to contracts |

---

## Status & Next

- **Live:** All EVM contracts (production + beta), Echomix privacy transport
- **In dev:** Aztec private voting, SubDAO treasury autonomy
- **Gap:** No on-chain SubDAO registry, no cross-chain coordination, Aztec proving not in production
