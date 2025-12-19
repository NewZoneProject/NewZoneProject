NZ-0038: Deterministic Consensus Rollback
Version: draft v0  
Status: Active  
Category: Consensus  

1. Purpose

This specification defines deterministic consensus rollback for the NewZone standard.  
Its purpose is to ensure that collective decisions can be rolled back in a provably unique, immutable, and formally verifiable way without reliance on randomness or probabilistic models.

---

2. Scope

This specification covers:

- deterministic rollback rules for consensus proofs  
- compatibility with deterministic consensus proofs (NZ‑0034)  
- integration with stateless transport rollback (NZ‑0035)  
- constraints ensuring predictability and formal verifiability  

This specification does not define transport replay (NZ‑0039).

---

3. Terminology

Consensus Rollback — deterministic restoration of consensus state to a prior valid proof.  
Invariant — condition that must always hold true.  
Rollback Binding — deterministic association between rollback and consensus proof.  

---

4. Principles

4.1 Determinism
Rollback must be identical across all implementations.

4.2 Minimalism
Only essential rollback rules may be used.

4.3 Predictability
Rollback must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
Rollback must resist quantum manipulation.

4.6 Independence
Rollback must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No probabilistic rollback.  
2. No time‑based validation.  
3. No adaptive or environment‑dependent metadata.  
4. No dynamic negotiation.  
5. All rollback rules must be deterministic and stable.  
6. Rollback must be forward‑compatible for decades.

---

6. Rollback Model

Each consensus rollback is defined as:

```
consensusrollback(groupid) = consensusproof(groupid, fixed_parameters)
```

Where:

- group_id = deterministic identifier of consensus group  
- fixed_parameters = immutable encoding rules (NZ‑0033)  
- consensus_proof = deterministic consensus proof (NZ‑0034)  

Forbidden:

- random salts  
- time‑based seeds  
- environment‑dependent entropy  

---

7. Rollback Rules

7.1 Rule 1 — Group Binding
Rollback must bind group_id to consensus proof.

7.2 Rule 2 — Fixed Parameters
Rollback must include fixed encoding parameters (NZ‑0033).

7.3 Rule 3 — Stateless Enforcement
Rollback must not maintain dynamic state beyond deterministic rules.

7.4 Rule 4 — Formal Proof Obligations
Rollback must be provably unique and loop‑free.

---

8. Formal Verification Requirements

Rollback must define:

- preconditions (valid group_id, valid encoding parameters)  
- postconditions (deterministic rollback output)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness, collision resistance)  

Compatible with NZ‑0008.

---

9. Security Considerations

- Malicious nodes must not influence rollback outputs.  
- Rollback must resist Grover’s algorithm.  
- Deterministic rules must prevent manipulation.  
- Rollback must be formally verifiable.

---

10. Future Work

- NZ‑0039 Stateless Transport Replay Model  
- NZ‑0040 Identity Graph Integrity Proofs  
- NZ‑0041 Metadata Compression Proofs  
- NZ‑0042 Deterministic Consensus Replay  

---

11. References

None.
