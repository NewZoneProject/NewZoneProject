# NZ-0004: Routing Protocol
Version: draft v0  
Status: Active  
Category: Core  

## 1. Purpose

This specification defines the conceptual routing protocol of the NewZone standard.  
Routing determines how nodes discover each other, how paths are formed, and how messages are delivered in a decentralized, durable, and deterministic manner.  
This document does not define transport‑level details or implementation‑specific algorithms.

---

## 2. Scope

This specification covers:

- the conceptual routing model  
- node discovery rules  
- path formation principles  
- routing constraints  
- terminology used across routing‑related specifications  

This specification does **not** define message formats, communication flows, or storage mechanisms.  
Those are defined in NZ‑0003 and NZ‑0005.

---

## 3. Terminology

**Node** — any entity participating in the network.  
**Route** — a deterministic path between two nodes.  
**Hop** — a single step in a route.  
**Neighbor** — a node directly reachable by another node.  
**Discovery** — the process of learning about other nodes.  
**Topology** — the logical structure of node connectivity.  
**Path Selection** — the process of choosing a route among available options.

---

## 4. Principles

### 4.1 Decentralization
Routing must not rely on centralized servers, authorities, or privileged nodes.

### 4.2 Determinism
Given the same topology, all nodes must derive identical routing decisions.

### 4.3 Minimalism
Routing metadata must be minimal and stable.

### 4.4 Durability
The routing model must remain valid for decades, independent of transport technologies.

### 4.5 Autonomy
Nodes must be able to operate in offline, intermittent, or degraded environments.

### 4.6 Predictability
Routing behavior must be transparent and reproducible.

---

## 5. Design Constraints

1. Routing must not depend on synchronized clocks.  
2. Routing must not assume global knowledge of the network.  
3. Routing must not rely on mutable external state.  
4. Routing metadata must be deterministic and minimal.  
5. Nodes must not assume stable connectivity.  
6. Routing must support dynamic topologies.  
7. Routing must avoid probabilistic or heuristic‑only decisions.  
8. Routing must be platform‑agnostic.

---

## 6. Routing Model

The NewZone routing model consists of three conceptual layers:

### 6.1 Discovery Layer
Nodes learn about other nodes through:

- direct communication  
- neighbor exchange  
- broadcast announcements  
- cached information  

Discovery must be deterministic and must not rely on centralized registries.

### 6.2 Path Formation Layer
Nodes construct routes using:

- identity fingerprints (NZ‑0002)  
- neighbor tables  
- deterministic selection rules  

Routes must be reproducible across implementations.

### 6.3 Path Selection Layer
Nodes choose routes based on:

- minimal hop count  
- deterministic tie‑breaking rules  
- stable identity ordering  

No probabilistic or machine‑learning‑based selection is allowed.

---

## 7. Routing Behavior

### 7.1 Direct Routing
If the destination is a known neighbor, the message is delivered directly.

### 7.2 Multi‑Hop Routing
If the destination is not a neighbor, the node selects the next hop using deterministic rules.

### 7.3 Broadcast Routing
Broadcast messages propagate through neighbors with loop‑prevention rules.

### 7.4 Degraded Routing
Nodes must continue routing even with partial or outdated topology information.

---

## 8. Routing Metadata

Routing metadata must include:

- sender identity  
- destination identity  
- hop counter  
- optional path trace  

Metadata must be minimal and must not expose sensitive information.

---

## 9. Security Considerations

- Nodes must validate routing metadata before forwarding.  
- Routing must assume adversarial environments.  
- Loop prevention must be deterministic.  
- Malicious nodes must not be able to influence global routing behavior.  
- Identity spoofing must be detectable by higher‑level specifications.

---

## 10. Future Work

- NZ‑0009 Message Envelope Format  
- NZ‑0011 Deterministic Path Selection Rules  
- NZ‑0012 Routing Table Compression  
- NZ‑0013 Offline Routing Strategies  

---

## 11. References

None.