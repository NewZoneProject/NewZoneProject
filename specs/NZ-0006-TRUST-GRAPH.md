# NZ-0006: Trust Graph
Version: draft v0  
Status: Active  
Category: Core  

## 1. Purpose

This specification defines the conceptual trust graph used in the NewZone standard.  
The trust graph enables nodes to evaluate the reliability, authenticity, and behavior of other nodes without relying on centralized authorities.  
It provides a deterministic, minimalistic, and durable model for decentralized trust.

---

## 2. Scope

This specification covers:

- the structure of the trust graph  
- trust relationships between nodes  
- rules for evaluating and updating trust  
- constraints ensuring determinism and autonomy  
- terminology used across trust‑related specifications  

This specification does **not** define cryptographic signatures, identity proofs, or consensus algorithms.  
Those are defined in later specifications.

---

## 3. Terminology

**Node** — any entity participating in the network.  
**Trust Edge** — a directional relationship representing trust from one node to another.  
**Trust Weight** — a deterministic value representing the strength of trust.  
**Trust Graph** — a directed graph composed of nodes and trust edges.  
**Reputation** — a derived measure of a node’s behavior over time.  
**Observation** — a recorded event affecting trust.

---

## 4. Principles

### 4.1 Decentralization
Trust must not rely on centralized authorities, servers, or privileged nodes.

### 4.2 Determinism
Given the same observations, all nodes must derive identical trust values.

### 4.3 Minimalism
Trust metadata must be minimal and stable.

### 4.4 Durability
The trust model must remain valid for decades, independent of cryptographic trends.

### 4.5 Transparency
Trust relationships must be explainable and reproducible.

### 4.6 Autonomy
Nodes must be able to evaluate trust independently, even in offline environments.

---

## 5. Design Constraints

1. Trust must be derived only from deterministic observations.  
2. Trust must not depend on external authorities or centralized registries.  
3. Trust values must be stable and platform‑agnostic.  
4. Trust updates must not rely on synchronized clocks.  
5. Trust must not depend on mutable global state.  
6. Trust must be explainable and reproducible.  
7. Trust must support adversarial environments.

---

## 6. Trust Graph Model

The trust graph consists of:

- nodes (identities from NZ‑0002)  
- directed trust edges  
- deterministic trust weights  
- derived reputation values  

### 6.1 Trust Edges

A trust edge is defined as:

- source node  
- target node  
- trust weight  
- optional observation reference  

Trust edges must be:

- deterministic  
- minimal  
- stable  
- explainable  

### 6.2 Trust Weights

Trust weights must:

- be deterministic  
- be derived from observations  
- be bounded within a predefined range  
- not rely on floating‑point arithmetic  
- not rely on probabilistic models  

### 6.3 Observations

Observations include:

- successful message exchanges  
- routing reliability  
- storage integrity  
- protocol compliance  
- detected malicious behavior  

Observations must be:

- deterministic  
- verifiable  
- platform‑agnostic  

---

## 7. Reputation Model

Reputation is derived from:

- incoming trust edges  
- outgoing trust edges  
- historical observations  
- deterministic aggregation rules  

Reputation must:

- be reproducible across implementations  
- not rely on centralized scoring  
- not rely on machine learning  
- not rely on probabilistic inference  

---

## 8. Trust Propagation

Trust may propagate through the graph using:

- deterministic path evaluation  
- bounded propagation depth  
- stable tie‑breaking rules  

Propagation must not:

- create infinite loops  
- amplify trust beyond defined limits  
- rely on global knowledge of the graph  

---

## 9. Security Considerations

- Trust must assume adversarial environments.  
- Malicious nodes must not be able to manipulate global trust.  
- Trust edges must be validated before use.  
- Observations must be verifiable and tamper‑resistant.  
- Trust decay must be deterministic and not time‑based.  
- Sybil attacks must be mitigated through deterministic rules.

---

## 10. Future Work

- NZ‑0018 Observation Format  
- NZ‑0019 Trust Weight Calculation Rules  
- NZ‑0020 Reputation Aggregation Model  
- NZ‑0021 Sybil Resistance Mechanisms  

---

## 11. References

None.