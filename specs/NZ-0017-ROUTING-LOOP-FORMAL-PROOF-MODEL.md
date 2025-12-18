NZ-0017: Routing Loop Formal Proof Model
Version: draft v0  
Status: Active  
Category: Core  

1. Purpose

This specification defines the formal proof model used to guarantee loop‑free routing in the NewZone standard.  
Its purpose is to ensure that all routing decisions, path selections, and table transformations are provably free of cycles, without relying on time, randomness, or dynamic measurements.

---

2. Scope

This specification covers:

- formal loop‑freedom definitions  
- deterministic proof obligations  
- invariants for routing tables and paths  
- compatibility with all routing‑related specifications  

This specification does not define routing algorithms themselves (NZ‑0004), only the proof model.

---

3. Terminology

Loop — a path where a node appears more than once.  
Cycle — a closed sequence of hops returning to the origin.  
Acyclic Path — a path with strictly increasing identity ordering.  
Invariant — a property that must always hold.  
Proof Obligation — a condition that must be proven true for correctness.

---

4. Principles

4.1 Determinism
Loop‑freedom must be provable using deterministic rules.

4.2 Minimalism
Only essential invariants may be used.

4.3 Predictability
Loop‑freedom must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
Proofs must not rely on cryptographic shortcuts vulnerable to quantum attacks.

4.6 Independence
Loop‑freedom must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No probabilistic or heuristic loop detection.  
2. No timestamps or time‑based behavior.  
3. No dynamic measurements.  
4. No environment‑dependent metadata.  
5. No reliance on synchronized clocks.  
6. All proofs must be deterministic.  
7. Loop‑freedom must be stable across decades.

---

6. Loop‑Freedom Definition

A path is loop‑free if and only if:

```
∀ i, j: i < j → identity[i] < identity[j]
```

Identity ordering is defined in NZ‑0002.

This ensures:

- strict monotonicity  
- no repeated nodes  
- no cycles  
- no ambiguous ordering  

---

7. Routing Invariants

The following invariants must hold for all routing tables and paths:

7.1 Invariant 1 — Identity Monotonicity
All paths must have strictly increasing identity sequences.

7.2 Invariant 2 — Deterministic Neighbor Ordering
Neighbor tables must follow NZ‑0013 ordering rules.

7.3 Invariant 3 — Deterministic Link Quality
Link quality must follow NZ‑0014 and must not introduce cycles.

7.4 Invariant 4 — Prefix Stability
Prefix groups (NZ‑0012) must not create overlapping identity ranges.

7.5 Invariant 5 — Expansion Stability
Expansion (NZ‑0015) must not introduce new identities or reorder paths.

7.6 Invariant 6 — Multi‑Path Stability
Multi‑path selection (NZ‑0016) must not include paths violating identity monotonicity.

---

8. Proof Obligations

Each routing component must satisfy the following obligations:

8.1 Path Selection (NZ‑0011)
Must prove:

```
selected_path is acyclic
```

8.2 Compression (NZ‑0012)
Must prove:

```
compression preserves acyclic structure
```

8.3 Expansion (NZ‑0015)
Must prove:

```
expanded_table preserves acyclic structure
```

8.4 Multi‑Path Selection (NZ‑0016)
Must prove:

```
∀ p in multipath_set: p is acyclic
```

8.5 Routing Protocol (NZ‑0004)
Must prove:

```
protocol transitions preserve invariants
```

---

9. Formal Loop‑Freedom Model

Loop‑freedom is proven using:

9.1 Identity‑Based Ordering
Identity ordering (NZ‑0002) forms a strict total order.

9.2 Path Weight Ordering
Path weights (NZ‑0011) enforce monotonicity.

9.3 Deterministic Neighbor Ordering
Neighbor tables (NZ‑0013) prevent ambiguous adjacency.

9.4 Deterministic Link Quality
Link quality (NZ‑0014) prevents nondeterministic path selection.

9.5 Deterministic Multi‑Path Rules
Multi‑path selection (NZ‑0016) prevents divergent cycles.

---

10. Security Considerations

- Malicious nodes must not influence identity ordering.  
- Loop‑freedom must not rely on unverifiable metadata.  
- Deterministic proofs must prevent routing manipulation.  
- Loop‑freedom must be formally verifiable.  
- No dynamic behavior may affect correctness.

---

11. Future Work

- NZ‑0061 Formal Loop‑Freedom Proofs  
- NZ‑0062 Identity‑Based Graph Theory Model  
- NZ‑0063 Deterministic Cycle Detection Algorithms  
- NZ‑0064 Multi‑Layer Loop‑Freedom Model  

---

12. References

None.
