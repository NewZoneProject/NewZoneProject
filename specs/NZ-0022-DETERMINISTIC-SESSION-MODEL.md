NZ-0022: Deterministic Session Model
Version: draft v0  
Status: Active  
Category: Transport  

1. Purpose

This specification defines the deterministic session model used in the NewZone standard.  
Its purpose is to provide a timeless, stateless, and formally verifiable framework for establishing and maintaining transport sessions without relying on time, randomness, or adaptive negotiation.

---

2. Scope

This specification covers:

- deterministic session identifiers  
- session construction rules  
- session invariants  
- compatibility with transport envelope (NZ‑0021)  

This specification does not define flow control (NZ‑0023) or hashing (NZ‑0024).

---

3. Terminology

Session — a deterministic association between two identities.  
Session ID — a static identifier derived from identity pairs.  
Session Flags — deterministic binary indicators.  
Identity Ordering — deterministic ordering of identities (NZ‑0002).

---

4. Principles

4.1 Determinism
Sessions must be identical across all implementations.

4.2 Minimalism
Only essential fields may be included.

4.3 Predictability
Session behavior must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
Session IDs must not rely on cryptographic shortcuts vulnerable to quantum attacks.

4.6 Independence
Sessions must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No timestamps or time‑based session lifetimes.  
2. No probabilistic or adaptive negotiation.  
3. No environment‑dependent metadata.  
4. No dynamic handshake.  
5. All session rules must be deterministic and stable.  
6. Sessions must be forward‑compatible for decades.

---

6. Session Structure

The session structure consists of:

```
session = {
    session_id,
    source_identity,
    destination_identity,
    session_flags
}
```

6.1 session_id
Derived deterministically:

```
sessionid = hash(identitypair)
```

Where hash is defined in NZ‑0024.

6.2 source_identity
Identity of the sender (NZ‑0002).

6.3 destination_identity
Identity of the receiver (NZ‑0002).

6.4 session_flags
Deterministic bitmask:

- integrity_required  
- compression_allowed  
- reservedfuturebits  

---

7. Forbidden Fields

Sessions must never include:

- timestamps  
- dynamic sequence numbers  
- probabilistic retransmit counters  
- congestion control metadata  
- environment‑dependent metadata  
- adaptive negotiation fields  

---

8. Deterministic Session Rules

8.1 Rule 1 — Identity Pairing
Sessions are defined strictly by identity pairs.

8.2 Rule 2 — Lexicographic Ordering
Identity pairs must be ordered lexicographically.

8.3 Rule 3 — Static Flags
Flags must be deterministic and globally defined.

8.4 Rule 4 — Statelessness
Sessions must not maintain dynamic state.

8.5 Rule 5 — Formal Proof Obligations
Sessions must be provably unique and loop‑free.

---

9. Formal Verification Requirements

Sessions must define:

- preconditions (valid identities)  
- postconditions (deterministic session)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of session_id)  

Compatible with NZ‑0008.

---

10. Security Considerations

- Malicious nodes must not influence session IDs.  
- Session flags must not leak sensitive information.  
- Deterministic rules must prevent manipulation.  
- Sessions must be formally verifiable.

---

11. Future Work

- NZ‑0023 Stateless Flow Control  
- NZ‑0024 Quantum‑Resilient Transport Hash  
- NZ‑0025 Fixed‑Width Transport Encoding  
- NZ‑0026 Deterministic Session Integrity Proofs  

---

12. References

None.
