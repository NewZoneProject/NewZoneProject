NZ-0023: Stateless Flow Control
Version: draft v0  
Status: Active  
Category: Transport  

1. Purpose

This specification defines the stateless flow control model used in the NewZone standard.  
Its purpose is to ensure predictable, timeless, and formally verifiable flow regulation without relying on time, randomness, or adaptive mechanisms.

---

2. Scope

This specification covers:

- deterministic flow control rules  
- static window definitions  
- compatibility with transport envelope (NZ‑0021) and sessions (NZ‑0022)  
- constraints ensuring predictability and formal verifiability  

This specification does not define hashing (NZ‑0024) or encoding (NZ‑0025).

---

3. Terminology

Flow Control — deterministic regulation of packet transmission.  
Static Window — fixed, deterministic bound on outstanding packets.  
Flow ID — deterministic identifier derived from identity pairs (NZ‑0022).  
Deterministic Ordering — lexicographic ordering of flows.

---

4. Principles

4.1 Determinism
Flow control must produce identical results for identical inputs.

4.2 Minimalism
Only essential rules may be used.

4.3 Predictability
Flow control must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
Flow IDs must not rely on cryptographic shortcuts vulnerable to quantum attacks.

4.6 Independence
Flow control must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No adaptive window sizing.  
2. No time‑based retransmit.  
3. No probabilistic congestion control.  
4. No environment‑dependent metadata.  
5. No reliance on synchronized clocks.  
6. All flow control rules must be deterministic.  
7. Flow control must be stable across decades.

---

6. Static Window Model

Each flow is assigned a static window:

```
staticwindow = fixedinteger
```

Where:

- fixed_integer is globally defined  
- must be identical across all implementations  
- must not depend on environment or time  

Forbidden:

- dynamic resizing  
- adaptive congestion control  
- probabilistic retransmit  

---

7. Flow Control Rules

7.1 Rule 1 — Flow Identification
Flows are identified deterministically by session_id (NZ‑0022).

7.2 Rule 2 — Window Enforcement
At most static_window packets may be outstanding per flow.

7.3 Rule 3 — Lexicographic Ordering
Flows must be scheduled lexicographically by flow_id.

7.4 Rule 4 — Stateless Enforcement
Flow control must not maintain dynamic state beyond static window counters.

7.5 Rule 5 — Formal Proof Obligations
Flow control must be provably unique and loop‑free.

---

8. Forbidden Mechanisms

Flow control must never include:

- adaptive congestion control  
- probabilistic retransmit  
- time‑based timers  
- environment‑dependent metadata  
- dynamic negotiation  

---

9. Formal Verification Requirements

Flow control must define:

- preconditions (valid session, valid flow_id)  
- postconditions (deterministic window enforcement)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of flow control state)  

Compatible with NZ‑0008.

---

10. Security Considerations

- Malicious nodes must not influence flow control windows.  
- Flow IDs must be collision‑resistant.  
- Deterministic rules must prevent manipulation.  
- Flow control must be formally verifiable.

---

11. Future Work

- NZ‑0024 Quantum‑Resilient Transport Hash  
- NZ‑0025 Fixed‑Width Transport Encoding  
- NZ‑0026 Deterministic Session Integrity Proofs  
- NZ‑0027 Stateless Flow Verification Model  

---

12. References

None.
