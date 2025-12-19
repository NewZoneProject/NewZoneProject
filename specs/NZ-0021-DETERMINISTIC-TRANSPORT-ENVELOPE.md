NZ-0021: Deterministic Transport Envelope
Version: draft v0  
Status: Active  
Category: Transport  

1. Purpose

This specification defines the deterministic transport envelope used in the NewZone standard.  
Its purpose is to provide a stable, timeless, and formally verifiable container for transporting payloads across the network, without relying on time, randomness, or dynamic state.

---

2. Scope

This specification covers:

- structure of the transport envelope  
- deterministic field definitions  
- compatibility with Message Envelope (NZ‑0009)  
- compatibility with Payload Schema (NZ‑0010)  
- constraints ensuring predictability and formal verifiability  

This specification does not define transport sessions (NZ‑0022) or flow rules (NZ‑0023).

---

3. Terminology

Transport Envelope — a deterministic container between the message envelope and payload.  
Transport Header — static metadata describing transport semantics.  
Transport Flags — deterministic binary indicators.  
Identity Ordering — deterministic ordering of identities (NZ‑0002).

---

4. Principles

4.1 Determinism
Transport envelopes must be identical across all implementations.

4.2 Minimalism
Only essential fields may be included.

4.3 Predictability
Transport behavior must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
Transport envelopes must not rely on cryptographic shortcuts vulnerable to quantum attacks.

4.6 Independence
Transport envelopes must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No timestamps or time‑based fields.  
2. No sequence numbers dependent on time.  
3. No probabilistic or adaptive fields.  
4. No environment‑dependent metadata.  
5. No dynamic negotiation.  
6. All fields must be deterministic and stable.  
7. Envelope must be forward‑compatible for decades.

---

6. Transport Envelope Structure

The transport envelope consists of:

```
transport_envelope = {
    transport_version,
    transport_flags,
    source_identity,
    destination_identity,
    flow_id,
    payload_type,
    payload_length
}
```

6.1 transport_version
A static integer identifying the transport envelope version.  
Must be deterministic and globally defined.

6.2 transport_flags
A deterministic bitmask:

- fragmentation_allowed  
- integrity_required  
- compression_allowed  
- reservedfuturebits  

Flags must be:

- deterministic  
- explicitly defined  
- lexicographically comparable  

6.3 source_identity
Identity of the sender (NZ‑0002).

6.4 destination_identity
Identity of the receiver (NZ‑0002).

6.5 flow_id
A deterministic identifier for grouping packets into flows.  
Must be derived from:

```
flowid = hash(identitypair, payload_type)
```

Where hash is a deterministic, quantum‑resilient, collision‑resistant mapping defined in NZ‑0024.

6.6 payload_type
Payload schema type (NZ‑0010).

6.7 payload_length
Static length of the payload in bytes.  
Must not depend on dynamic fragmentation.

---

7. Forbidden Fields

The transport envelope must never include:

- timestamps  
- TTL or hop‑based timers  
- dynamic sequence numbers  
- probabilistic retransmit counters  
- congestion control metadata  
- environment‑dependent metadata  
- adaptive negotiation fields  

These violate determinism and formal verifiability.

---

8. Deterministic Encoding Rules

8.1 Rule 1 — Lexicographic Field Ordering
Fields must be encoded in strict lexicographic order by field name.

8.2 Rule 2 — Fixed‑Width Encoding
All fields must use fixed‑width encoding defined in NZ‑0025.

8.3 Rule 3 — No Optional Fields
Optional fields introduce nondeterminism.

8.4 Rule 4 — No Compression of Header
Only payload may be compressed.

---

9. Formal Verification Requirements

Transport envelopes must define:

- preconditions (valid identities, valid payload type)  
- postconditions (deterministic envelope)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of envelope encoding)  

Compatible with NZ‑0008.

---

10. Security Considerations

- Malicious nodes must not influence envelope structure.  
- Flow IDs must be collision‑resistant.  
- Transport flags must not leak sensitive information.  
- Deterministic rules must prevent manipulation.  
- Envelope must be formally verifiable.

---

11. Future Work

- NZ‑0022 Deterministic Session Model  
- NZ‑0023 Stateless Flow Control  
- NZ‑0024 Quantum‑Resilient Transport Hash  
- NZ‑0025 Fixed‑Width Transport Encoding  

---

12. References

None.
