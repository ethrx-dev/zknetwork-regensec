# 02 — Local Private AI

> ZK-verified edge inference. Intelligence that can be trusted without being surveilled.

## Purpose

AI inference across the stack is designed for verifiability and privacy. The Funion protocol provides ZK-verifiable inference proofs — a node can prove it ran a specific model on specific input without revealing the input, the output, or the operator. The Echomix mixnet is optionally available as a transport layer for applications that also need metadata unlinkability.

## Components

### 2a. Funion — Anonymous Inference Protocol

**Path:** `zknet-0AI/opt/server_plugins/ai_inference/`

| Plugin | Language | Purpose |
|--------|----------|---------|
| `service.go` | Go | Main AI inference service |
| `funion_client.go` | Go | Funion protocol client |
| `mix_client.go` | Go | Optional mixnet transport integration |
| `sphinx.go` | Go | Optional Sphinx packet encryption |
| `vllm_engine.go` | Go | vLLM inference engine |
| `zk_verifier.go` | Go | ZK proof verification for inference |
| `bacap.go` | Go | Bandwidth/capacity management |
| `latency_bucket.go` | Go | Timing obfuscation |
| `storage_client.go` | Go | Anonymous storage of input tensors |
| `config.go` | Go | Service configuration |

### 2b. zerOAI Engine

**Path:** `opt/zknode-zerOAI/`

| Component | Purpose |
|-----------|---------|
| Docker Compose | Full node stack: walletshield, ant-node, kairos, validator, zerOAI, monitoring |
| zerOAI service | AI inference engine on edge node |
| TRINITY_MIXMESH_INFERENCE.md | Mixmesh inference architecture (optional transport) |

### 2c. Gaia AI Agents (Edge)

**Path:** `zknet-farmtech/src/pages/AIAdvisor.jsx`

| Agent | Function |
|-------|----------|
| Plant Health | Predicts disease, nutrient deficiencies from sensor data |
| Harvest Timing | Optimizes harvest schedule |
| Energy Management | Predicts solar production, manages consumption |
| Anomaly Detection | Learns normal patterns, alerts on deviations |
| Educational Assistant | Personalized learning guidance |

---

## Interfaces

| Interface | With Layer | Mechanism |
|-----------|------------|-----------|
| Inference from sensor data | 05 Sensor Layer | Funion anonymous RPC |
| Proof of inference | 04 ZK Application Layer | Noir circuit for inference verification |
| Storage of tensors/results | 03 Post-Quantum Storage | Content-addressed blob |
| Model updates | 01 Coordination Layer | Governance-approved model distribution |

---

## Status & Next

- **Built:** Funion Go plugins, zerOAI deployment spec, Gaia AI in FarmTech
- **Gap:** No on-device training, no federated learning, no proof-of-inference circuit deployed, no quantized model pipeline
- **Next:** Wire Funion to live node, deploy proof-of-inference Noir circuit, ship quantized models to edge
