NZ-0046: Deterministic Consensus Integrity Proofs
Version: draft v0  
Status: Active  
Category: Consensus  

1. Purpose

This specification defines deterministic integrity proofs for consensus processes in the NewZone standard.  
Its purpose is to ensure that consensus states remain provably intact, immutable, and formally verifiable across all implementations.

---

2. Scope

This specification covers:

- deterministic integrity proofs for consensus states (NZ‑0034)  
- compatibility with deterministic consensus rollback (NZ‑0038)  
- integration with deterministic consensus replay (NZ‑0042)  
- constraints ensuring predictability and formal verifiability  

This specification does not define transport replay proofs (NZ‑0047).

---

3. Terminology

Consensus Integrity Proof — deterministic evidence that a consensus state has not been altered.  
Invariant — condition that must always hold true.  
Proof Binding — deterministic association between consensus state and proof artifact.  

---

4. Principles

4.1 Determinism
Integrity proofs must be identical across all implementations.

4.2 Minimalism
Only essential consensus fields may be included.

4.3 Predictability
Proofs must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
Proofs must preserve hash integrity against quantum attacks.

4.6 Independence
Proofs must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No probabilistic proofs.  
2. No time‑based validation.  
3. No adaptive or environment‑dependent metadata.  
4. No dynamic negotiation.  
5. All proof rules must be deterministic and stable.  
6. Proofs must be forward‑compatible for decades.

---

6. Integrity Proof Model

Each consensus integrity proof is defined as:

```
consensusproof(stateid) = consensushash(stateid, fixed_parameters)
```

Where:

- state_id = deterministic identifier of consensus state  
- fixed_parameters = immutable encoding rules (NZ‑0033)  
- consensus_hash = deterministic consensus hash (NZ‑0034)  

Forbidden:

- random salts  
- time‑based seeds  
- environment‑dependent entropy  

---

7. Integrity Proof Rules

7.1 Rule 1 — State Binding
Proof must bind state_id to consensus state.

7.2 Rule 2 — Fixed Parameters
Proof must include fixed encoding parameters (NZ‑0033).

7.3 Rule 3 — Stateless Enforcement
Proof must not maintain dynamic state beyond deterministic rules.

7.4 Rule 4 — Formal Proof Obligations
Proof must be provably unique and loop‑free.

---

8. Formal Verification Requirements

Integrity proof must define:

- preconditions (valid state_id, valid encoding parameters)  
- postconditions (deterministic proof output)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness, collision resistance)  

Compatible with NZ‑0008.

---

9. Security Considerations

- Malicious nodes must not influence proof outputs.  
- Proofs must resist Grover’s algorithm.  
- Deterministic rules must prevent manipulation.  
- Proofs must be formally verifiable.

---

10. Future Work

- NZ‑0047 Stateless Transport Replay Proofs  
- NZ‑0048 Identity Graph Integrity Replay Proofs  
- NZ‑0049 Metadata Integrity Replay Proofs  
- NZ‑0050 Deterministic Consensus Replay Proofs  

---

11. References

None.
