NZ-0019: Deterministic Packet Classification
Version: draft v0  
Status: Active  
Category: Core  

1. Purpose

This specification defines the deterministic packet classification model used in the NewZone standard.  
Its purpose is to ensure that all packets are classified in a predictable, stable, and formally verifiable manner before forwarding decisions are applied.

---

2. Scope

This specification covers:

- deterministic packet classification  
- field extraction rules  
- class ordering  
- compatibility with routing and forwarding specifications  

This specification does not define forwarding (NZ‑0018) or routing (NZ‑0004).

---

3. Terminology

Packet Class — a deterministic category assigned to a packet.  
Classification Key — a tuple of extracted fields.  
Envelope — the outer message container (NZ‑0009).  
Payload Schema — the inner structure (NZ‑0010).  
Deterministic Ordering — lexicographic ordering of classification keys.

---

4. Principles

4.1 Determinism
Classification must produce identical results for identical packets.

4.2 Minimalism
Only essential fields may be used.

4.3 Predictability
Classification must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
Classification must not rely on cryptographic shortcuts vulnerable to quantum attacks.

4.6 Independence
Classification must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No probabilistic classification.  
2. No time‑based classification.  
3. No dynamic or adaptive behavior.  
4. No environment‑dependent metadata.  
5. No reliance on synchronized clocks.  
6. All classification rules must be deterministic.  
7. Classification must be stable across decades.

---

6. Classification Key

The classification key is a deterministic tuple:

```
classification_key = (
    envelope_type,
    payload_type,
    source_identity,
    destination_identity,
    hop_count
)
```

Where:

- envelope_type is defined in NZ‑0009  
- payload_type is defined in NZ‑0010  
- sourceidentity and destinationidentity follow NZ‑0002  
- hop_count is a static, deterministic field (not time‑based)

Forbidden:

- timestamps  
- dynamic counters  
- random values  
- environment‑dependent fields  

---

7. Packet Classes

Packets are classified into the following deterministic classes:

7.1 Class 0 — Control
Routing, neighbor, and verification messages.

7.2 Class 1 — System
System‑level payloads defined by NZ‑0010.

7.3 Class 2 — Application
Application‑level payloads.

7.4 Class 3 — Extended
Future‑reserved deterministic classes.

Classes must be ordered lexicographically by:

1. class_id  
2. classification_key  

---

8. Classification Rules

8.1 Rule 1 — Extract Envelope Fields
Extract envelope type and identities.

8.2 Rule 2 — Extract Payload Fields
Extract payload type.

8.3 Rule 3 — Construct Classification Key
Construct the deterministic tuple.

8.4 Rule 4 — Determine Class
Use envelopetype and payloadtype to assign class.

8.5 Rule 5 — Deterministic Ordering
Packets must be processed in lexicographic order of:

```
(classid, classificationkey)
```

8.6 Rule 6 — No Dynamic Reordering
Forbidden:

- priority queues  
- adaptive scheduling  
- time‑based reordering  
- probabilistic reordering  

---

9. Formal Verification Requirements

Classification must define:

- preconditions (valid envelope, valid payload)  
- postconditions (deterministic class assignment)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of classification)  

Compatible with NZ‑0008.

---

10. Security Considerations

- Malicious nodes must not influence classification order.  
- Classification must not leak sensitive information.  
- Deterministic rules must prevent manipulation.  
- Classification must be formally verifiable.

---

11. Future Work

- NZ‑0069 Deterministic Packet Scheduling  
- NZ‑0070 Multi‑Layer Classification Model  
- NZ‑0071 Stateless Classification Proofs  
- NZ‑0072 Deterministic QoS Model  

---

12. References

None.
