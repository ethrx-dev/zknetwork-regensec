# 01 — Secured Intention Coordination

> The substrate for aligned, verifiable collective action. Intentions are cryptographically committed, ZK-verified, and executed without intermediaries.

## Essence

This layer is the **Secured Intention Coordination Protocol** — the mechanism by which humans, agents, DAOs, and infrastructure nodes translate intention into coordinated action with cryptographic guarantees. Every action on this layer is:

- **Intention-anchored** — proposals, votes, and economic signals specify *what* is intended before *how* it is executed
- **ZK-verifiable** — every state transition can be proven correct without revealing sensitive context
- **Sovereign by design** — participants can exit at any time, taking their proofs, assets, and agency
- **Metadata-private** — optional privacy transport available for applications that need unlinkability

The Credo of ZKNetwork is not decorative — it is encoded into the governance mechanisms themselves. Every proposal, every vote, every treasury action is subject to automated Credo Alignment Checks.

## Credo Principles as Governance Mechanisms

| Principle | Governance Mechanism |
|-----------|---------------------|
| **Trustlessness** | All protocol actions produce ZK-verifiable proofs. Smart contracts and governance logic are open-source, version-controlled, cryptographically signed. New technical modules require verifiable proof of intended function. |
| **Sovereignty** | Fork-ready architecture with low-cost exit. Multi-sig treasury control across diverse participants. Every new dependency passes an "exit viability" review. |
| **Selective Disclosure** | Governance rights verified through ZK proofs without revealing wallet addresses. Compliance uses ZK attestations, not raw data. Anonymous proposal submission via privacy transport. |
| **Metadata Privacy by Default** | All DAO-approved applications enable metadata privacy at the protocol layer. Proposals include a "metadata privacy score." Optional mix-net integration for communication channels. |
| **Multi-Chain & Modular** | Chain-agnostic standards (Intention ERC). Governance modules designed for external DAOs to fork and adapt. Interchain voting hooks across L1s and L2s. |
| **Intent-Centric Coordination** | All proposals specify intent in structured format for AI/agent interpretation. Delegated AI agents bound by cryptographically verifiable intent contracts. Intention-to-execution audit via ZK proofs. |
| **Aligned With Nature** | Ecosystem impact reports, diversity metrics in governance, feedback loop requirements on all major initiatives. |
| **Resistance to Oppression** | Oppression impact assessments, fail-safe standards, community-supervised kill switch. |
| **AI-Ready & AI-Safe** | Agent registration with ZK compliance proofs. AI output verification for governance-affecting systems. Commons protection against extractive agent behaviors. |
| **Conway's Law Awareness** | Org-to-protocol mapping: working groups map to protocol modules. Cross-functional design reviews. Transparent, privacy-preserving governance archives. |

These are enforced by the **Meta-Governance Protocol**, which validates proposals against Credo-aligned schemas, runs automated AI agents to flag misalignments, and publishes periodic Governance Integrity Reports with ZK proofs of adherence.

## Core Protocol: Proof of Useful Work (PoUW)

PoUW is the regenerative consensus mechanism of the Secured Intention Coordination layer. Unlike proof of work (energy waste) or proof of stake (capital concentration), PoUW rewards verifiable real-world contributions. It is the economic primitive that aligns self-interest with collective benefit — every reward is backed by a ZK proof of useful action.

### PoUW Reward Classes

| Class | Contribution | Proof Source | ZK Circuit |
|-------|--------------|-------------|------------|
| **Node Operations** | Uptime, bandwidth, compute relay | Node attestation, mixnet participation | `uptime.nr` |
| **Food Production** | Verifiable food output from Micro-Greenhouse Kits | CircuitTree sensor data | `food_output.nr` |
| **Data Contribution** | Sensor data for AI training, climate reporting, network health | Signed sensor streams | `data_contribution.nr` |
| **Education** | Skill completion, Learn-to-Earn module mastery | zkID credential attestation | `skill_proof.nr` |
| **Governance** | Vote participation, proposal creation, SubDAO contributions | On-chain governance actions | `governance_proof.nr` |
| **AI Compute** | Anonymous inference execution via Funion | Proof-of-inference circuit | `inference_proof.nr` |
| **Storage** | Data persistence, replication, availability | Proof-of-storage circuit | `storage_proof.nr` |

### PoUW Protocol Flow

```
05 Sensor Layer (data)
    → 04 ZK Layer (Noir proof generation)
    → 01 Secured Intention Coordination (proof submission)
    → PoUW Verifier contract (proof verification)
    → TokenomicsRouter (reward distribution)
    → zkID (private reward claim)
```

### PoUW and the Credo

| Credo Principle | PoUW Alignment |
|----------------|----------------|
| Trustlessness | Every reward is ZK-verifiable without a trusted intermediary |
| Sovereignty | Proofs are portable — operators can exit with their contribution history |
| Aligned With Nature | Rewards regenerative activity instead of extractive or wasteful computation |
| Resistance to Oppression | No central authority can deny rewards — the protocol pays out automatically |
| Intent-Centric | Rewards are based on intended, verified outcomes, not speculative position |

### Code Location

| Component | Path |
|-----------|------|
| PoUW circuits (Noir) | `zknet-labs/templates/zkapp-template/circuits/src/pouw.nr` (template) |
| PoUW verifier (contract) | To be deployed: `ZKNGovenance.sol` extension or dedicated `PoUWVerifier.sol` |
| PoUW engine (client) | `zknfa-framework/src/services/pouw.js` |
| PoUW reward types | `zknfa-framework/src/services/rewards.js` |
| NFA spec with PoUW layer | `zknet-labs/NFA-Specification.md` |

## Components

### 1a. Smart Contracts — Production

**Path:** `zkn-contracts/contracts/`

| Contract | Purpose | Credo Alignment |
|----------|---------|-----------------|
| ZKNToken | ERC20 with mint, burn, snapshots, pausable, vesting | Trustlessness, Sovereignty |
| TokenomicsRouter | Revenue split: treasury, staking, grants, liquidity | Multi-Chain, Regenerative |
| ZKNGovenance | Proposal lifecycle, operator-weighted voting, 5 proposal types | Intent-Centric, Selective Disclosure |
| YieldVault | Staking with time-based multipliers, auto-compounding | Aligned With Nature (feedback loops) |
| ZKNTreasury | Stable-to-ZKN conversion with lockup | Sovereignty (exit-ready) |
| RevenuePool | Continuous payment streams | Trustlessness |
| GrantPool | Milestone-based grant disbursement | Intent-Centric, Resistance to Oppression |
| LiquidityReserve | Uniswap LP management | Multi-Chain |
| ZKNDeployer | Atomic factory deployment | Modular |

### 1b. Smart Contracts — Beta

**Path:** `zkn-ecosystem/contracts/`

| Contract | Purpose |
|----------|---------|
| ZKNBeta | ZKNB token with airdrop |
| StakingVault | Staking with operator multipliers |
| NodeOperator | Agent registration, bonding, reputation |
| RevenueRouter | Stablecoin revenue distribution |
| Treasury | Stable-to-ZKNB conversion |
| GrantPool | Milestone-based grants |
| LiquidityReserve | Uniswap LP for ZKNB-stable |
| ZKNEcosystemDeployer | Factory deployment |

### 1c. Private Governance Circuits (Noir / Aztec)

**Path:** `aztec-ballot/contracts/`

| Circuit | Purpose |
|---------|---------|
| Private Voting | Ballot creation, secret cast, ZK tally |
| Agent Registry | Private identity/agent registry |
| Operations | Operational logic circuits |

### 1d. DAO Governance Framework

**Path:** `ZKN-SRC/src/dao/`

| Document | Purpose |
|----------|---------|
| ZKN-DAO-Ordinance.md | Foundational governance ordinance |
| ZKN-DAO-Governance-Guidebook.md | Operational guidebook |
| ZKN-SubDAO-Interop-Model.md | SubDAO interoperability |
| ZKN-Credo-GovOps-Alignment-Guide.md | Credo-to-governance mapping |
| ZKN-DAO-Phase1-Op-Checklist.md | Launch checklist |

### 1e. Meta-Governance Protocol

The Meta-Governance Protocol is the enforcement layer for Credo alignment:

- Validates proposal formats against Credo-aligned schemas
- Runs automated AI agents to flag principle misalignments
- Publishes periodic Governance Integrity Reports with ZK proofs
- Allows community veto of proposals that materially violate the Credo

### 1f. Privacy Transport (Optional Module)

**Path:** `opt/pki/`, `zknet-labs/katzenpost/`

The Echomix metadata-private communication substrate — optional transport for SubDAOs and applications requiring unlinkability. Available as a modular privacy layer, not a core requirement.

| Subcomponent | Status |
|-------------|--------|
| Directory Authorities (PKI) | 🟢 Live (3 nodes, VPS) |
| Mix nodes (x3) | 🟢 Live (VPS) |
| Gateway node | 🟢 Live (VPS) |
| Service node + http_proxy plugin | 🟢 Live (VPS) |
| Courier (Pigeonhole) | 🟢 Live (VPS) |
| Configuration generator | 🟢 Ready |

## Interfaces

| Outbound | To Layer | Mechanism |
|----------|----------|-----------|
| PoUW reward payouts | 04 ZK Layer (zkID) | TokenomicsRouter → zkID after proof verification |
| PoUW proof submission | 04 ZK Layer | Noir proof → PoUW Verifier → TokenomicsRouter |
| Governance decisions | 05 Sensor Layer | Encrypted channel → zerOS |
| Proof verification | 04 ZK Layer | ZK proof submission to contracts |
| Intention broadcast | All layers | On-chain intent signals → AI agent execution |

## Status & Next

- **Live:** All EVM contracts (production + beta), Echomix privacy transport
- **In dev:** Aztec private voting, SubDAO treasury autonomy, Meta-Governance Protocol
- **Gap:** No on-chain SubDAO registry, no cross-chain coordination, Credo Alignment Checks not automated in production
- **Next:** Deploy SubDAO factory with embedded Credo checks, wire Aztec private voting, build Meta-Governance enforcement pipeline
