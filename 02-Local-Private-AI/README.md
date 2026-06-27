# 02 — Local Private AI

> Anonymous edge inference. Intelligence without surveillance. AI that runs on hardware you own.

## Purpose

All AI inference in ZKNetwork is designed to be private (no data leaves the node without ZK protection) and local (no cloud dependency). The Funion protocol provides sender-receiver unlinkability for AI queries. Gaia agents run on-device models for real-time decisions.

## Components

### 2a. Funion — Anonymous AI Inference

**Path:** `zknet-0AI/opt/server_plugins/ai_inference/`

The core anonymous inference protocol. Uses Echomix mixnet for provable unlinkability between query sender and inference result.

| Plugin Component | Language | Purpose |
|-----------------|----------|---------|
| `service.go` | Go | Main AI inference service |
| `funion_client.go` | Go | Funion protocol client |
| `mix_client.go` | Go | Mixnet integration |
| `sphinx.go` | Go | Sphinx packet encryption |
| `vllm_engine.go` | Go | vLLM inference engine integration |
| `zk_verifier.go` | Go | ZK proof verification for inference |
| `bacap.go` | Go | Bandwidth/capacity management |
| `charlie_service.go` | Go | Charlie service node |
| `latency_bucket.go` | Go | Timing obfuscation — quantized execution into public latency buckets |
| `storage_client.go` | Go | Anonymous storage of input tensors |
| `config.go` | Go | Service configuration |

### 2b. zerOAI Engine

**Path:** `opt/zknode-zerOAI/`

Production node deployment with AI inference capabilities.

| Component | Purpose |
|-----------|---------|
| Docker Compose | Full stack: kpclientd-tunnel, walletshield, ant-node, kairos, validator, zerOAI, monitoring |
| zerOAI service | AI inference engine on edge node |
| Prometheus/Loki/Grafana/Tempo | Observability stack |
| TRINITY_MIXMESH_INFERENCE.md | Mixmesh inference architecture doc |

### 2c. Gaia AI Agents (Edge)

**Path:** `zknet-farmtech/src/pages/AIAdvisor.jsx`

On-device AI agents running on the ZK Secure IO Controller.

| Agent | Function |
|-------|----------|
| Plant Health | Predicts disease, nutrient deficiencies from sensor data |
| Harvest Timing | Optimizes harvest schedule based on growth models |
| Energy Management | Predicts solar production, manages consumption |
| Anomaly Detection | Learns normal patterns, alerts on deviations |
| Educational Assistant | Personalized learning guidance |

### 2d. Learn-to-Earn AI

**Path:** `zknet-farmtech/src/pages/LearnToEarn.jsx`

AI-powered educational curriculum with token rewards for skill completion.

---

## Interfaces

| Interface | With Layer | Mechanism |
|-----------|------------|-----------|
| Inference requests from sensors | 05 Sensor Layer | Funion anonymous RPC |
| Proof generation for AI results | 04 ZK Application Layer | Noir circuits for inference verification |
| Storage of tensors/results | 03 Post-Quantum Storage | Anonymous tensor storage via Pigeonhole |
| Model updates from DAO | 01 Coordination Layer | Governance-approved model distribution |

---

## Status & Next

- **Built:** Funion Go plugins (service, client, vLLM, ZK verifier, latency buckets, storage client)
- **Built:** zerOAI Docker Compose deployment, Gaia AI page in FarmTech
- **Gap:** No on-device model training (only inference), no federated learning, no proof-of-inference yet, no quantized model deployment pipeline
- **Next:** Ship quantized models to edge, wire Funion plugins to live mixnet, build anonymous LLM query UI in clients
