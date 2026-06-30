# 05 — Secure Hardware Layer

> Hardware root of trust. zerOS hardened edge runtime. The physical interface where data becomes provable.

## Purpose

This layer is the hardware substrate of the stack — the physically anchored trust root. The zymbit HSM provides tamper-resistant key storage and hardware-backed signing. zerOS provides a hardened, immutable Linux runtime. The ZK Secure IO Controller is the edge compute brain that runs zerOS, collects sensor data, executes AI models, and generates ZK proofs. Everything in this layer is designed to produce cryptographically verifiable statements about the physical world — anchored to hardware that cannot be compromised without physical evidence.

## Components

### 5a. Zymbit Hardware Security Module (HSM)

**Path:** `SYSTEM.md`, `opt/zknode-zerOAI/`

Hardware root of trust for all cryptographic operations on the edge node.

| Capability | Status |
|-----------|--------|
| ECDSA signing (slot 21) | 🟢 Live (CM4) |
| BIP39 master seed (slot 16) | 🟢 Live (CM4) |
| Deterministic key derivation | 🟢 Live |
| Tamper-responsive key erasure | 🟡 Spec'd |
| Remote attestation | 🟡 In design |

### 5b. zerOS Hardened Linux

**Path:** `ZerOSv2/ZerOS-Build-Specification.md`

Security-hardened Linux operating system for edge deployment. Provides the secure runtime environment for all software on the node.

| Feature | Status |
|---------|--------|
| Secure boot with verified boot chain | 🟡 Spec'd |
| Immutable root filesystem | 🟡 Spec'd |
| Hardware-backed key storage (zymbit) | 🟢 Live |
| Physical tamper detection | 🟡 Spec'd |
| Encrypted auto-updates via secure channel | 🟡 Spec'd |
| Offline-first operation | 🟡 Spec'd |

### 5c. ZK Secure IO Controller

**Path:** `ZKN-SRC/src/ops/ZKN-AI-Powered-Micro-Greenhouse-Product.md`

The edge compute brain of every ZKN hardware node. Runs zerOS, hosts the zymbit HSM, and provides the compute environment for all node operations.

| Capability | Status |
|-----------|--------|
| Runs zerOS hardened Linux | 🟡 Spec'd |
| Hosts zymbit HSM for key operations | 🟢 Live (CM4) |
| Executes local AI models (Gaia) | 🟡 Spec'd |
| Collects encrypted sensor data | 🟡 Spec'd |
| Generates ZK proofs from sensor data | 🟡 In design |
| Routes data through optional privacy transport | 🟡 Spec'd |

### 5d. CircuitTree IoT Sensor Suite

**Path:** `Micro-Greenhouse_Kit_Component_Reference.md`

Environmental sensors that feed data into the ZK proof pipeline.

| Sensor | Measurement | Status |
|--------|-------------|--------|
| Soil moisture | Moisture content | 🟡 Spec'd |
| pH sensor | Soil pH | 🟡 Spec'd |
| Temperature | Ambient temperature | 🟡 Spec'd |
| Humidity | Relative humidity | 🟡 Spec'd |
| Ambient light | PAR/light intensity | 🟡 Spec'd |
| CO2 concentration | Atmospheric CO2 | 🟡 Spec'd |
| Nutrient flow rate | Hydroponic flow | 🟡 Spec'd |
| Water level | Reservoir level | 🟡 Spec'd |

### 5e. Micro-Greenhouse Kit

**Path:** `Micro-Greenhouse_Kit_for_Civic_Resilience.md`

The flagship deployment vehicle — a complete, programmable civic infrastructure node built on the secure hardware stack.

| Subsystem | Purpose |
|-----------|---------|
| ZK Secure IO Controller (zerOS + zymbit) | Edge compute, HSM, proof generation |
| CircuitTree sensors | Environmental monitoring |
| Solar power system | Energy sovereignty |
| FarmOS | Farm management software |
| Mesh transport | Infrastructure-independent connectivity |

### 5f. FarmTech Application

**Path:** `zknet-farmtech/`

Tauri desktop application for managing the Micro-Greenhouse Kit.

| Page | Function |
|------|----------|
| FarmDashboard | Farm overview |
| SeedToHarvest | Crop lifecycle |
| GreenhouseManager | Environmental controls |
| CropPlanner | Rotation planning |
| SensorHub | IoT sensor data |
| HarvestLog | Harvest recording |
| AIAdvisor | AI recommendations |
| MarketPage | Farm-to-market |
| LearnToEarn | Education + rewards |
| FarmRewards | Token incentives |
| FarmGovernance | DAO governance |

### 5g. Live Physical Deployment (zknode01)

**Path:** `SYSTEM.md`

| Hardware | Role | Location |
|----------|------|----------|
| CM4 (zknode01) | ZK Secure IO Controller (zerOS target) | 192.168.9.118 |
| zymbit (slot 21) | Hardware HSM — transaction signing, key storage | CM4 |
| VPS | Network infrastructure (authorities, transport nodes) | 217.60.7.200 |

---

## Interfaces

| Interface | With Layer | Mechanism |
|-----------|------------|-----------|
| Send sensor data for proof generation | 04 ZK Stack | Encrypted CBOR → Noir circuit RPC |
| Hardware-signed transactions | 01 Secured Intention Coordination | zymbit → WalletShield (optional) → on-chain |
| Request AI inference | 02 Local Private AI | Funion anonymous RPC |
| Receive governance commands | 01 Secured Intention Coordination | Encrypted channel → zerOS update system |
| Store encrypted data | 03 Post-Quantum Storage | Content-addressed blob |

---

## Status & Next

- **Live:** CM4 with zymbit HSM, FarmTech app built, live monitoring
- **Spec'd:** zerOS, CircuitTree sensors, Micro-Greenhouse Kit, ZK Secure IO Controller
- **Gap:** No zerOS image built (CM4 runs standard Debian), no sensors integrated, no physical greenhouse, zymbit tamper-response not configured
- **Next:** Build zerOS image for CM4 (Yocto/Buildroot), integrate CircuitTree sensors, wire zymbit attestation into boot chain, prototype first greenhouse
