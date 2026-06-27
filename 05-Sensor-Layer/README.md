# 05 — Sensor Layer

> The physical world interface. Hardware root of trust. Where bits meet biology.

## Purpose

This layer is where ZKNetwork touches the physical world. Sensors collect environmental data (soil, air, water, energy). The ZK Secure IO Controller processes it at the edge. zerOS provides a hardened operating system. The Micro-Greenhouse Kit is the flagship deployment vehicle. Mesh networking ensures connectivity independence.

## Components

### 5a. ZK Secure IO Controller

**Path:** `ZKN-SRC/src/ops/ZKN-AI-Powered-Micro-Greenhouse-Product.md`

The edge compute brain of every ZKN hardware node.

| Capability | Status |
|-----------|--------|
| Runs zerOS hardened Linux | 🟡 Spec'd |
| Executes local AI models (Gaia) | 🟡 Spec'd |
| Collects encrypted sensor data | 🟡 Spec'd |
| Routes traffic through mixnet | 🟡 Spec'd |
| Tamper-resistant key storage (zymkey) | 🟢 Live (CM4) |
| FarmOS farm management | 🟡 Spec'd |

### 5b. zerOS Hardened Linux

**Path:** `ZerOSv2/ZerOS-Build-Specification.md`

Security-hardened Linux for edge deployment.

| Feature | Status |
|---------|--------|
| Secure boot with verified boot chain | 🟡 Spec'd |
| Immutable root filesystem | 🟡 Spec'd |
| Hardware-backed key storage | 🟢 Live (zymkey on CM4) |
| Tamper detection | 🟡 Spec'd |
| Encrypted auto-updates via mixnet | 🟡 Spec'd |

### 5c. CircuitTree IoT Sensor Suite

**Path:** `Micro-Greenhouse_Kit_Component_Reference.md`

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

### 5d. Micro-Greenhouse Kit

**Path:** `Micro-Greenhouse_Kit_for_Civic_Resilience.md`, `ZKN-SRC/src/ops/`

The flagship physical deployment — a complete, programmable civic infrastructure node.

| Subsystem | Purpose |
|-----------|---------|
| ZK Secure IO Controller | Edge compute + mixnet routing |
| CircuitTree sensors | Environmental monitoring |
| Solar power system | Energy sovereignty |
| FarmOS | Farm management software |
| Mesh networking (Reticulum) | Infrastructure-independent connectivity |
| Grow system | Hydroponic/aquaponic food production |

### 5e. FarmTech Application

**Path:** `zknet-farmtech/`

Tauri desktop app for greenhouse management.

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

### 5f. Mesh Networking

**Path:** `opt/zerOS/`, `ZKN-SRC/src/ops/The-Peoples-DePIN.md`

| Protocol | Role |
|----------|------|
| Reticulum | Encrypted mesh transport |
| Echomix mixnet | Privacy layer over mesh |
| WiFi / LoRa | Physical radio layer |

### 5g. Live Physical Deployment (zknode01)

**Path:** `SYSTEM.md`

| Hardware | Role | Location |
|----------|------|----------|
| CM4 (zknode01) | Edge compute + WalletShield + Autonomi | 192.168.9.118 |
| zymkey (slot 21) | Hardware signing | CM4 |
| VPS | Mixnet authorities, nodes, gateway | 217.60.7.200 |

---

## Interfaces

| Interface | With Layer | Mechanism |
|-----------|------------|-----------|
| Send encrypted sensor data | 04 ZK Layer | CBOR over local bus → proof generation |
| Request AI inference | 02 AI Layer | Funion anonymous RPC |
| Receive governance commands | 01 Coordination Layer | Mixnet → zerOS update channel |
| Store data off-chain | 03 Storage Layer | Pigeonhole / Autonomi |

---

## Status & Next

- **Live:** CM4 deployment with WalletShield, zymkey, Autonomi; FarmTech app built; live monitoring
- **Spec'd:** zerOS, CircuitTree sensors, Micro-Greenhouse Kit, Secure IO Controller
- **Gap:** No physical greenhouse deployed (only spec + software), no sensor hardware integrated, mesh networking not deployed, zerOS not built from spec
- **Next:** Prototype first Micro-Greenhouse Kit with CM4 + CircuitTree sensors, build zerOS image, deploy FarmTech on live CM4, wire sensor data through full stack to on-chain proof
