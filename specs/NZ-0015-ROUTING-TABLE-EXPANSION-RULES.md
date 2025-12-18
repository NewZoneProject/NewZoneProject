NZ-0015: Routing Table Expansion Rules
Version: draft v0  
Status: Active  
Category: Core  

1. Purpose

This specification defines deterministic routing table expansion rules for the NewZone standard.  
Its purpose is to ensure that compressed routing tables (NZ‑0012) can be expanded into full routing tables in a deterministic, reversible, and formally verifiable manner.

---

2. Scope

This specification covers:

- deterministic expansion of prefix groups  
- reconstruction of full routing tables  
- constraints ensuring predictability and formal verifiability  
- terminology used across routing‑related specifications  

This specification does not define compression rules (NZ‑0012) or path selection (NZ‑0011).

---

3. Terminology

Compressed Table — a routing table containing prefix groups.  
Expanded Table — a full routing table with explicit destination → next hop entries.  
Prefix Group — a deterministic grouping of identities with shared structural properties.  
Identity Ordering — deterministic ordering of node identities (NZ‑0002).  
Lossless Expansion — expansion that preserves all routing semantics.

---

4. Principles

4.1 Determinism
Expansion must produce identical results for identical inputs.

4.2 Minimalism
Only essential information may be used during expansion.

4.3 Losslessness
Expansion must fully restore the original routing semantics.

4.4 Formal Verifiability
Expansion rules must be expressible in formal logic.

4.5 Quantum Resilience
Expansion must not rely on cryptographic shortcuts vulnerable to quantum attacks.

4.6 Independence
Expansion must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No probabilistic or heuristic expansion.  
2. No timestamps or time‑based behavior.  
3. No randomness or entropy sources.  
4. No environment‑dependent metadata.  
5. No reliance on synchronized clocks.  
6. All expansion rules must be deterministic.  
7. Expansion must be reversible (lossless).  
8. Expansion must be stable across decades.

---

6. Expansion Rules

Expansion proceeds in the following deterministic order:

6.1 Rule 1 — Identify Prefix Groups
For each prefix entry:

- extract prefix  
- extract next hop  
- determine identity range covered by the prefix  

6.2 Rule 2 — Enumerate Covered Identities
Using NZ‑0002 identity structure:

- enumerate all identities matching the prefix  
- ordering must be lexicographic  
- enumeration must be deterministic and complete  

6.3 Rule 3 — Generate Explicit Entries
For each enumerated identity:

```
destination → next_hop
```

6.4 Rule 4 — Merge With Explicit Entries
If the compressed table contains explicit entries:

- explicit entries override prefix‑derived entries  
- conflicts must not occur (NZ‑0012 guarantees this)  

6.5 Rule 5 — Deterministic Ordering
Expanded entries must be ordered lexicographically by:

1. destination identity  
2. next hop identity  

6.6 Rule 6 — Stable Expansion
Expansion must not introduce:

- new prefixes  
- new metadata  
- new routing semantics  

---

7. Reversibility Requirements

Expansion must allow:

- deterministic reconstruction of the full table  
- deterministic validation of prefix coverage  
- deterministic comparison with compressed form  

Reversibility must not require external metadata.

---

8. Formal Verification Requirements

Expansion must define:

- preconditions (valid compressed table)  
- postconditions (deterministic expanded table)  
- invariants (no ambiguity, no overlap)  
- proof obligations (reversibility, determinism)  

All rules must be compatible with NZ‑0008.

---

9. Security Considerations

- Expansion must assume adversarial environments.  
- Malicious nodes must not influence prefix enumeration.  
- Identity spoofing must be detectable by higher‑level specifications.  
- Expansion must not leak sensitive information.  
- Deterministic rules must prevent routing manipulation.

---

10. Future Work

- NZ‑0053 Prefix Enumeration Model  
- NZ‑0054 Identity Range Compression  
- NZ‑0055 Multi‑Layer Expansion Rules  
- NZ‑0056 Formal Expansion Proofs  

---

11. References

None.