NZ-0016: Multi-Path Deterministic Selection
Version: draft v0  
Status: Active  
Category: Core  

1. Purpose

This specification defines deterministic multi-path selection rules for the NewZone standard.  
Its purpose is to enable nodes to select multiple valid routes to a destination without relying on randomness, probability, or dynamic measurements.  
All selected paths must be stable, predictable, and formally verifiable.

---

2. Scope

This specification covers:

- deterministic multi-path selection  
- ordering and filtering rules  
- constraints ensuring predictability and formal verifiability  
- terminology used across routing‑related specifications  

This specification does not define path discovery or transport mechanisms.

---

3. Terminology

Candidate Path — a possible route to the destination.  
Primary Path — the first selected path (NZ‑0011).  
Secondary Path — any additional selected path.  
Path Weight — deterministic tuple describing path cost.  
Identity Ordering — deterministic ordering of node identities (NZ‑0002).

---

4. Principles

4.1 Determinism
Given identical inputs, all nodes must derive identical multi-path sets.

4.2 Minimalism
Only essential rules may be used.

4.3 Predictability
Multi-path selection must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
No rule may rely on cryptographic shortcuts vulnerable to quantum attacks.

4.6 Independence
Selection must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No probabilistic or heuristic selection.  
2. No timestamps or time‑based behavior.  
3. No randomness or entropy sources.  
4. No environment‑dependent metadata.  
5. No reliance on synchronized clocks.  
6. All selection rules must be deterministic.  
7. Multi-path sets must be stable across decades.

---

6. Path Weight Model

Each path is assigned a deterministic weight:

```
path_weight = (
    hop_count,
    max_identity,
    identity_sequence,
    first_hop,
    lastintermediatehop
)
```

This is identical to NZ‑0011, ensuring compatibility.

Comparison is lexicographic.

---

7. Multi-Path Selection Rules

Multi-path selection proceeds in the following deterministic order:

7.1 Rule 1 — Select Primary Path
Use NZ‑0011 to select the primary path.

7.2 Rule 2 — Filter Candidate Paths
Remove all paths that:

- contain loops  
- violate identity ordering  
- violate deterministic neighbor table rules (NZ‑0013)  
- violate link quality rules (NZ‑0014)

7.3 Rule 3 — Sort Remaining Paths
Sort all remaining paths lexicographically by:

1. path_weight  
2. full identity sequence  

7.4 Rule 4 — Select Secondary Paths
Select all paths whose path_weight satisfies:

```
pathweight <= primarypathweight + deterministicthreshold
```

Where:

- deterministic_threshold is a fixed, static integer  
- threshold must be identical across all implementations  
- threshold must not depend on environment or time  

7.5 Rule 5 — Stable Ordering
The final multi-path set must be ordered lexicographically.

7.6 Rule 6 — No Dynamic Limits
The number of selected paths must not depend on:

- time  
- load  
- environment  
- heuristics  

Only deterministic rules may influence the final set.

---

8. Deterministic Threshold Model

The threshold must:

- be static  
- be globally defined  
- be independent of environment  
- be formally verifiable  

Example (allowed):

```
deterministic_threshold = 1
```

Forbidden:

- adaptive thresholds  
- probabilistic thresholds  
- time‑based thresholds  
- environment‑dependent thresholds  

---

9. Formal Verification Requirements

Multi-path selection must define:

- preconditions (valid candidate paths)  
- postconditions (deterministic multi-path set)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of selected set)  

All rules must be compatible with NZ‑0008.

---

10. Security Considerations

- Malicious nodes must not influence path ordering.  
- Identity spoofing must be detectable by higher‑level specifications.  
- Deterministic thresholds must prevent manipulation.  
- Multi-path sets must not leak sensitive information.  
- Selection must be formally verifiable.

---

11. Future Work

- NZ‑0057 Multi-Path Compression Rules  
- NZ‑0058 Multi-Path Integrity Format  
- NZ‑0059 Multi-Path Formal Proofs  
- NZ‑0060 Deterministic Load Distribution  

---

12. References

None.
