NZ-0042: Deterministic Consensus Replay
Version: draft v0  
Status: Active  
Category: Consensus  

1. Purpose

This specification defines deterministic replay rules for consensus proofs in the NewZone standard.  
Its purpose is to allow consensus states to be replayed in a provably unique, immutable, and formally verifiable way without reliance on randomness or hidden state.

---

2. Scope

This specification covers:

- deterministic replay of consensus proofs (NZ‑0034)  
- compatibility with deterministic consensus rollback (NZ‑0038)  
- integration with stateless transport replay (NZ‑0039)  
- constraints ensuring predictability and formal verifiability  

This specification does not define transport integrity proofs (NZ‑0043).

---

3. Terminology

Consensus Replay — deterministic reproduction of consensus state.  
Invariant — condition that must always hold true.  
Replay Binding — deterministic association between replay and consensus proof.  

---

4. Principles

4.1 Determinism
Replay must be identical across all implementations.

4.2 Minimalism
Only essential consensus data may be replayed.

4.3 Predictability
Replay must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
Replay must resist quantum manipulation.

4.6 Independence
Replay must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No probabilistic replay.  
2. No time‑based validation.  
3. No adaptive or environment‑dependent metadata.  
4. No dynamic negotiation.  
5. All replay rules must be deterministic and stable.  
6. Replay must be forward‑compatible for decades.

---

6. Replay Model

Each consensus replay is defined as:

```
consensusreplay(groupid) = consensusproof(groupid, fixed_parameters)
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

7. Replay Rules

7.1 Rule 1 — Group Binding
Replay must bind group_id to consensus proof.

7.2 Rule 2 — Fixed Parameters
Replay must include fixed encoding parameters (NZ‑0033).

7.3 Rule 3 — Stateless Enforcement
Replay must not maintain dynamic state beyond deterministic rules.

7.4 Rule 4 — Formal Proof Obligations
Replay must be provably unique and loop‑free.

---

8. Formal Verification Requirements

Replay must define:

- preconditions (valid group_id, valid encoding parameters)  
- postconditions (deterministic replay output)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness, collision resistance)  

Compatible with NZ‑0008.

---

9. Security Considerations

- Malicious nodes must not influence replay outputs.  
- Replay must resist Grover’s algorithm.  
- Deterministic rules must prevent manipulation.  
- Replay must be formally verifiable.

---

10. Future Work

- NZ‑0043 Stateless Transport Integrity Proofs  
- NZ‑0044 Identity Graph Replay Model  
- NZ‑0045 Metadata Replay Model  
- NZ‑0046 Deterministic Consensus Integrity Proofs  

---

11. References

None.
