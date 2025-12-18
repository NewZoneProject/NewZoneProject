# NZ-0014: Deterministic Link Quality Derivation
Version: draft v0  
Status: Active  
Category: Core  

## 1. Purpose

This specification defines the deterministic derivation rules for link quality in the NewZone standard.  
Its purpose is to ensure that all nodes compute identical link quality values given identical inputs, enabling predictable routing, formal verifiability, and long‑term stability.

---

## 2. Scope

This specification covers:

- deterministic link quality derivation  
- allowed and forbidden metrics  
- constraints ensuring predictability and formal verifiability  
- terminology used across routing‑related specifications  

This specification does **not** define neighbor discovery or transport mechanisms.

---

## 3. Terminology

**Link Quality** — a deterministic metric describing the cost or weight of a link.  
**Static Metric** — a value that does not depend on time or randomness.  
**Capability Flag** — a deterministic binary indicator of supported features.  
**Identity Ordering** — deterministic ordering of node identities (NZ‑0002).

---

## 4. Principles

### 4.1 Determinism  
Given identical inputs, all nodes must derive identical link quality values.

### 4.2 Minimalism  
Only essential, stable metrics may be used.

### 4.3 Predictability  
Link quality must be transparent and reproducible.

### 4.4 Formal Verifiability  
All derivation rules must be expressible in formal logic.

### 4.5 Quantum Resilience  
No metric may rely on cryptographic shortcuts vulnerable to quantum attacks.

### 4.6 Independence  
Link quality must not depend on time, randomness, or external state.

---

## 5. Design Constraints

1. No timestamps or time‑based metrics.  
2. No probabilistic or random values.  
3. No dynamic measurements (latency, jitter, packet loss, bandwidth).  
4. No environment‑dependent metadata.  
5. No reliance on synchronized clocks.  
6. All metrics must be deterministic and stable.  
7. Link quality must be comparable lexicographically.  
8. Derivation must be reversible and formally verifiable.

---

## 6. Allowed Metrics

Link quality may be derived from the following deterministic components:

### 6.1 Static Hop Cost  
A fixed integer representing the base cost of a hop.

### 6.2 Capability Flags  
A deterministic bitmask representing supported features:

- relay capability  
- storage capability  
- compression capability  
- quantum‑resilient capability  
- routing table compression capability  

Flags must be:

- deterministic  
- explicitly defined  
- lexicographically comparable  

### 6.3 Identity‑Aligned Weight  
A deterministic weight derived from the neighbor’s identity (NZ‑0002):

- lexicographic identity rank  
- prefix‑based structural weight  
- identity class weight  

Identity‑aligned weights must not leak sensitive information.

---

## 7. Forbidden Metrics

The following metrics must **never** be used:

- latency  
- jitter  
- packet loss  
- bandwidth  
- throughput  
- signal strength  
- dynamic measurements  
- probabilistic estimations  
- time‑dependent values  
- environment‑dependent values  

These violate determinism and formal verifiability.

---

## 8. Derivation Formula

Link quality must be computed as a deterministic tuple:

```
link_quality = (
    statichopcost,
    capability_flags,
    identity_weight
)
```

Comparison is lexicographic:

1. static_hop_cost  
2. capability_flags  
3. identity_weight  

This ensures:

- determinism  
- stability  
- formal verifiability  
- compatibility with NZ‑0013  
- compatibility with NZ‑0011  

---

## 9. Formal Verification Requirements

Link quality derivation must define:

- preconditions (valid identity, valid flags)  
- postconditions (deterministic tuple)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of derived value)  

All rules must be compatible with NZ‑0008.

---

## 10. Security Considerations

- Malicious nodes must not influence link quality through nondeterministic metadata.  
- Capability flags must be validated by higher‑level specifications.  
- Identity‑aligned weights must not leak sensitive information.  
- Deterministic derivation must prevent routing manipulation.  
- Link quality must be formally verifiable.

---

## 11. Future Work

- NZ‑0049 Capability Flag Registry  
- NZ‑0050 Identity‑Aligned Weight Specification  
- NZ‑0051 Link Quality Integrity Format  
- NZ‑0052 Formal Link Quality Proofs  

---

## 12. References

None.