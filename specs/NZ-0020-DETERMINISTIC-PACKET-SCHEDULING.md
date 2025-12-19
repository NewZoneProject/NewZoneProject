NZ-0020: Deterministic Packet Scheduling
Version: draft v0  
Status: Active  
Category: Core  

1. Purpose

This specification defines the deterministic packet scheduling model used in the NewZone standard.  
Its purpose is to ensure that packets are scheduled for forwarding in a predictable, stable, and formally verifiable manner, without relying on time, randomness, or adaptive behavior.

---

2. Scope

This specification covers:

- deterministic scheduling rules  
- ordering of classified packets  
- compatibility with forwarding (NZ‑0018)  
- constraints ensuring predictability and formal verifiability  

This specification does not define classification (NZ‑0019) or forwarding (NZ‑0018).

---

3. Terminology

Scheduling Queue — a deterministic, lexicographically ordered list of packets.  
Scheduling Key — a tuple derived from classification (NZ‑0019).  
Forwarding Decision — the next hop selection (NZ‑0018).  
Deterministic Ordering — strict lexicographic ordering.

---

4. Principles

4.1 Determinism
Scheduling must produce identical results for identical packet sets.

4.2 Minimalism
Only essential fields may influence scheduling.

4.3 Predictability
Scheduling must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
Scheduling must not rely on cryptographic shortcuts vulnerable to quantum attacks.

4.6 Independence
Scheduling must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No probabilistic scheduling.  
2. No time‑based scheduling.  
3. No dynamic priority adjustments.  
4. No environment‑dependent metadata.  
5. No reliance on synchronized clocks.  
6. All scheduling rules must be deterministic.  
7. Scheduling must be stable across decades.

---

6. Scheduling Key

The scheduling key is a deterministic tuple:

```
scheduling_key = (
    class_id,
    classification_key,
    source_identity,
    destination_identity
)
```

Where:

- class_id is defined in NZ‑0019  
- classification_key is the tuple from NZ‑0019  
- identities follow NZ‑0002  

Forbidden:

- timestamps  
- dynamic counters  
- random values  
- environment‑dependent fields  

---

7. Scheduling Rules

7.1 Rule 1 — Construct Scheduling Queue
All packets must be inserted into a single deterministic queue.

7.2 Rule 2 — Lexicographic Ordering
Packets must be ordered by:

1. class_id  
2. classification_key  
3. source_identity  
4. destination_identity  

7.3 Rule 3 — No Dynamic Reordering
Forbidden:

- priority queues  
- adaptive scheduling  
- time‑based reordering  
- probabilistic reordering  

7.4 Rule 4 — Deterministic Dequeue
The next packet to forward is always:

```
queue[0]
```

7.5 Rule 5 — Deterministic Failover
If the packet cannot be forwarded:

```
remove packet
continue with queue[1]
```

7.6 Rule 6 — Stateless Scheduling
Scheduling must not depend on:

- packet history  
- traffic patterns  
- load  
- timers  

---

8. Scheduling State Model

Scheduling state must be:

- stateless with respect to time  
- independent of packet history  
- independent of traffic patterns  
- derived solely from classification  

Forbidden:

- per‑flow state  
- per‑packet counters  
- timers  
- adaptive behavior  

---

9. Formal Verification Requirements

Scheduling must define:

- preconditions (valid classification)  
- postconditions (deterministic ordering)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of scheduling order)  

Compatible with NZ‑0008.

---

10. Security Considerations

- Malicious nodes must not influence scheduling order.  
- Scheduling must not leak sensitive information.  
- Deterministic rules must prevent manipulation.  
- Scheduling must be formally verifiable.

---

11. Future Work

- NZ‑0073 Deterministic Queue Integrity Format  
- NZ‑0074 Multi‑Layer Scheduling Model  
- NZ‑0075 Stateless Scheduling Proofs  
- NZ‑0076 Deterministic QoS Framework  

---

12. References

None.
