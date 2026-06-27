# 05 — Sensor Layer

> The physical world interface. Where sensor data becomes ZK proofs.

## Purpose

This layer translates physical events into verifiable data. Sensors collect environmental measurements. The ZK Secure IO Controller processes them at the edge and generates ZK proofs. zerOS provides a hardened runtime. The Micro-Greenhouse Kit is the flagship deployment. Everything in this layer is designed to produce verifiable statements about the physical world — without revealing more than necessary.

## Components

### 5a. ZK Secure IO Controller

**Path:** `ZKN-SRC/src/ops/ZKN-AI-Powered-Micro-Greenhouse-Product.md`

| Capability | Status |
|-----------|--------|
| Executes local AI models (Gaia) | 🟡 Spec'd |
| Collects encrypted sensor data | 🟡 Spec'd |
| Runs zerOS hardened Linux | 🟡 Spec'd |
| Tamper-resistant key storage (zymkey) | 🟢 Live (CM4) |
| Generates ZK proofs from sensor data | 🟡 In design |

### 5b. zerOS Hardened Linux

**Path:** `ZerOSv2/ZerOS-Build-Specification.md`

| Feature | Status |
|---------|--------|
| Secure boot with verified boot chain | 🟡 Spec'd |
| Immutable root filesystem | 🟡 Spec'd |
| Hardware-backed key storage | 🟢 Live (zymkey on CM4) |
| Tamper detection | 🟡 Spec'd |
| Encrypted auto-updates | 🟡 Spec'd |

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

**Path:** `Micro-Greenhouse_Kit_for_Civic_Resilience.md`

The flagship physical deployment vehicle.

| Subsystem | Purpose |
|-----------|---------|
| ZK Secure IO Controller | Edge compute + proof generation |
| CircuitTree sensors | Environmental monitoring |
| Solar power system | Energy sovereignty |
| FarmOS | Farm management software |
| Mesh transport | Infrastructure-independent connectivity |

### 5e. FarmTech Application

**Path:** `zknet-farmtech/`

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

---

## Interfaces

| Interface | With Layer | Mechanism |
|-----------|------------|-----------|
| Send sensor data for proof generation | 04 ZK Layer | Encrypted CBOR → Noir circuit |
| Request AI inference | 02 AI Layer | Funion anonymous RPC |
| Receive governance commands | 01 Coordination Layer | Encrypted channel → zerOS |
| Store data | 03 Storage Layer | Content-addressed blob |

---

## Status & Next

- **Live:** CM4 deployment with zymkey, FarmTech app built
- **Spec'd:** zerOS, CircuitTree sensors, Micro-Greenhouse Kit, Secure IO Controller
- **Gap:** No physical greenhouse deployed, no sensor hardware integrated, zerOS not built from spec
- **Next:** Prototype first Micro-Greenhouse Kit, build sensor → ZK proof pipeline, deploy FarmTech on live CM4
