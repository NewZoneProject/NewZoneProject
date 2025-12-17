# NZ-0011: Deterministic Path Selection Rules
Version: draft v0  
Status: Active  
Category: Core  

## 1. Purpose

This specification defines the deterministic rules used to select routing paths in the NewZone standard.  
Its purpose is to ensure that all nodes, given identical topology information, always derive the same routing decisions.  
The rules must be minimalistic, platform‑agnostic, formally verifiable, and durable for decades.

---

## 2. Scope

This specification covers:

- deterministic path selection rules  
- tie‑breaking mechanisms  
- constraints ensuring predictability and formal verifiability  
- terminology used across routing‑related specifications  

This specification does **not** define discovery, routing metadata, or transport mechanisms.

---

## 3. Terminology

**Route** — a deterministic sequence of hops from source to destination.  
**Hop** — a single step in a route.  
**Neighbor Table** — a deterministic list of known neighbors.  
**Candidate Path** — a possible route to the destination.  
**Tie‑Breaker** — a deterministic rule applied when multiple paths are equivalent.  
**Identity Ordering** — deterministic ordering of node identities (NZ‑0002).

---

## 4. Principles

### 4.1 Determinism  
Given identical inputs, all nodes must derive identical outputs.

### 4.2 Minimalism  
Path selection must use the smallest viable set of rules.

### 4.3 Predictability  
Routing decisions must be transparent and reproducible.

### 4.4 Formal Verifiability  
All rules must be expressible in formal logic.

### 4.5 Quantum Resilience  
Path selection must not rely on cryptographic shortcuts vulnerable to quantum attacks.

### 4.6 Independence  
Path selection must not depend on time, randomness, or external state.

---

## 5. Design Constraints

1. No probabilistic or heuristic decisions.  
2. No timestamps or time‑based behavior.  
3. No randomness or entropy sources.  
4. No environment‑dependent metadata.  
5. No reliance on synchronized clocks.  
6. All tie‑breakers must be deterministic.  
7. All rules must be stable across decades.

---

## 6. Path Selection Rules

Path selection proceeds in the following deterministic order:

### 6.1 Rule 1 — Minimal Hop Count  
Select the path with the smallest number of hops.

### 6.2 Rule 2 — Minimal Maximum Identity  
If multiple paths have the same hop count, select the path whose **maximum node identity** (NZ‑0002) is lexicographically smallest.

### 6.3 Rule 3 — Minimal Identity Sequence  
If still tied, compare the full identity sequences of the paths lexicographically.

### 6.4 Rule 4 — Minimal First Hop  
If still tied, select the path whose first hop has the lexicographically smallest identity.

### 6.5 Rule 5 — Minimal Last Hop Before Destination  
If still tied, select the path whose last intermediate hop has the lexicographically smallest identity.

### 6.6 Rule 6 — Stable Ordering  
If still tied, apply stable ordering based on:

- deterministic neighbor table ordering  
- deterministic candidate path ordering  

No additional rules may be introduced.

---

## 7. Tie‑Breaking Model

Tie‑breaking must:

- be deterministic  
- be stable across implementations  
- not rely on randomness  
- not rely on time  
- not rely on external state  
- be formally verifiable  

Tie‑breaking must not introduce new metadata or modify existing routing structures.

---

## 8. Formal Verification Requirements

Path selection must define:

- preconditions (valid topology, valid identities)  
- postconditions (deterministic path)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of selected path)  

All rules must be compatible with NZ‑0008.

---

## 9. Security Considerations

- Path selection must assume adversarial environments.  
- Malicious nodes must not influence deterministic ordering.  
- Identity spoofing must be detectable by higher‑level specifications.  
- Path selection must not leak sensitive information.  
- Deterministic rules must prevent routing manipulation.

---

## 10. Future Work

- NZ‑0037 Deterministic Neighbor Table Format  
- NZ‑0038 Path Compression Rules  
- NZ‑0039 Multi‑Path Deterministic Selection  
- NZ‑0040 Formal Routing Proofs  

---

## 11. References

None.