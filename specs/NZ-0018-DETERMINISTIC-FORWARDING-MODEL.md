NZ-0018: Deterministic Forwarding Model
Version: draft v0  
Status: Active  
Category: Core  

1. Purpose

This specification defines the deterministic forwarding model used in the NewZone standard.  
Its purpose is to ensure that packet forwarding is predictable, stable, loop‑free, and formally verifiable across all implementations, without relying on time, randomness, or dynamic measurements.

---

2. Scope

This specification covers:

- deterministic forwarding rules  
- next‑hop selection  
- multi‑path forwarding behavior  
- constraints ensuring predictability and formal verifiability  

This specification does not define routing table construction (NZ‑0004) or path selection (NZ‑0011, NZ‑0016).

---

3. Terminology

Forwarding Decision — deterministic selection of next hop for a packet.  
Primary Path — the first path selected by NZ‑0011.  
Secondary Paths — additional paths selected by NZ‑0016.  
Forwarding Set — the set of next hops eligible for forwarding.  
Deterministic Ordering — lexicographic ordering of identities.

---

4. Principles

4.1 Determinism
Forwarding must produce identical results for identical inputs.

4.2 Minimalism
Only essential information may influence forwarding.

4.3 Predictability
Forwarding behavior must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
Forwarding must not rely on cryptographic shortcuts vulnerable to quantum attacks.

4.6 Independence
Forwarding must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No probabilistic forwarding.  
2. No time‑based forwarding.  
3. No dynamic load balancing.  
4. No environment‑dependent metadata.  
5. No reliance on synchronized clocks.  
6. All forwarding rules must be deterministic.  
7. Forwarding must be stable across decades.  
8. Forwarding must preserve loop‑freedom (NZ‑0017).

---

6. Forwarding Set Construction

The forwarding set is constructed as follows:

6.1 Rule 1 — Primary Path Inclusion
The next hop of the primary path must always be included.

6.2 Rule 2 — Secondary Path Inclusion
Include next hops of all secondary paths selected by NZ‑0016.

6.3 Rule 3 — Deduplication
If multiple paths share the same next hop, include it only once.

6.4 Rule 4 — Deterministic Ordering
Order the forwarding set lexicographically by next hop identity.

---

7. Forwarding Rules

Forwarding proceeds in the following deterministic order:

7.1 Rule 1 — Single‑Path Case
If the forwarding set contains exactly one next hop:

```
forward(packet, next_hop)
```

7.2 Rule 2 — Multi‑Path Case
If the forwarding set contains multiple next hops:

```
forward(packet, forwarding_set[0])
```

Where:

- forwarding_set[0] is the lexicographically smallest next hop  
- no rotation, no hashing, no load balancing  

7.3 Rule 3 — Deterministic Failover
If the selected next hop becomes invalid:

```
forward(packet, nextvalidhopinorder)
```

7.4 Rule 4 — No Dynamic Behavior
Forwarding must not:

- rotate next hops  
- distribute load  
- adapt to conditions  
- use randomness  

7.5 Rule 5 — Loop‑Freedom
Forwarding must preserve all invariants defined in NZ‑0017.

---

8. Forwarding State Model

Forwarding state must be:

- stateless with respect to time  
- independent of packet history  
- independent of traffic patterns  
- derived solely from routing tables  

Forbidden:

- per‑flow state  
- per‑packet counters  
- timers  
- adaptive behavior  

---

9. Formal Verification Requirements

Forwarding must define:

- preconditions (valid routing table, valid forwarding set)  
- postconditions (deterministic next hop)  
- invariants (no randomness, no ambiguity, no loops)  
- proof obligations (uniqueness of forwarding decision)  

All rules must be compatible with NZ‑0008.

---

10. Security Considerations

- Malicious nodes must not influence forwarding order.  
- Forwarding must not leak sensitive information.  
- Deterministic rules must prevent manipulation.  
- Forwarding must be formally verifiable.  
- No dynamic behavior may affect correctness.

---

11. Future Work

- NZ‑0065 Deterministic Forwarding Integrity Format  
- NZ‑0066 Multi‑Layer Forwarding Model  
- NZ‑0067 Stateless Forwarding Proofs  
- NZ‑0068 Deterministic Packet Classification  

---

12. References

None.
