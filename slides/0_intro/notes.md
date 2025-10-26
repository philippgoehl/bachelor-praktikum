# Introduction

## Machine Learning (ML)

Machine Learning (ML) builds statistical models that learn patterns from data to make predictions or decisions with minimal manual rules.
In the classic setup, organizations centralize data on a server or cloud, train a model with algorithms, evaluate the model and iterate to reduce error while preventing overfitting.

Common paradigms include:

- supervised learning (labeled examples)
- unsupervised learning (structure discovery)
- reinforcement learning (trial-and-error policies).

Centralized ML is simple to manage and often achieves strong accuracy, but it requires collecting data—raising privacy, compliance, bandwidth, and latency concerns.

## Federated Learning (FL)

Federated Learning (FL) is a distributed ML approach where model training happens where the data resides (e.g., phones, hospitals, edge devices).
Instead of uploading raw data to a central server, participating clients compute local model updates and send only metadata (e.g., gradients or weights) to a coordinating server, which aggregates them into a new global model and broadcasts it back for the next training round.

### Why FL?

**Privacy by design**: No raw data leaves the device; only model updates are shared. This reduces, but does not eliminate, privacy risk. Practitioners typically add secure aggregation, differential privacy, and robust aggregation to harden guarantees.

**Regulatory alignment**: With the EU AI Act (in force since 01-08-2024), organizations face stronger requirements around data governance, transparency, and risk management. FL can support compliance by minimizing central data collection and improving data provenance and access control.

**Efficiency & scale**: Training leverages decentralized compute, lowering server load and network transfer.

**Speed**: Frequent aggregation rounds enable “exchange of learning progress,” often shortening time-to-improvement compared to waiting for periodic central uploads.

**Ubiquity of edge devices**: In the age of mobile and IoT, over half of the world’s population owns a smartphone (≈54% in 2023), making on-device learning broadly feasible.

### Typical use cases

- On-device personalization (keyboards, recommendations) without uploading sensitive user text or behavior.
- Cross-institution healthcare or finance, where data cannot leave premises but joint models are valuable.
- Industrial/IoT settings with limited bandwidth or intermittent connectivity.
