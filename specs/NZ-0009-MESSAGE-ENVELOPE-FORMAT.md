# NZ-0009: Message Envelope Format
Version: draft v0  
Status: Active  
Category: Core  

## 1. Purpose

This specification defines the deterministic message envelope format used across the NewZone standard.  
The envelope provides the minimal metadata required for message interpretation, routing, trust evaluation, and formal verification.  
It must remain stable, minimalistic, and platform‑agnostic for decades.

---

## 2. Scope

This specification covers:

- the structure of the message envelope  
- required and optional fields  
- deterministic encoding rules  
- constraints ensuring durability and quantum resilience  
- terminology used across message‑related specifications  

This specification does **not** define payload structure or serialization formats.

---

## 3. Terminology

**Envelope** — the minimal metadata required to interpret a message.  
**Payload** — the content of the message.  
**Sender** — the identity of the node that created the message.  
**Receiver** — the intended identity of the target node.  
**Flow ID** — an optional identifier for multi‑step interactions.  
**Message Type** — a deterministic classification of the message.  
**Integrity Tag** — a deterministic integrity check.

---

## 4. Principles

### 4.1 Minimalism
The envelope must contain only essential metadata.

### 4.2 Determinism
The same input must always produce the same envelope representation.

### 4.3 Portability
The envelope must be representable in plain text or binary formats.

### 4.4 Durability
The envelope format must remain stable for decades.

### 4.5 Quantum Resilience
The envelope must not expose metadata vulnerable to quantum‑accelerated attacks.

### 4.6 Formal Verifiability
All fields must be explicitly defined and verifiable.

---

## 5. Design Constraints

1. No timestamps or environment‑dependent fields.  
2. No probabilistic or random values.  
3. No implicit defaults — all fields must be explicit.  
4. No reliance on synchronized clocks.  
5. No platform‑specific metadata.  
6. All fields must be deterministic and stable.  
7. Integrity must be verifiable without external dependencies.

---

## 6. Envelope Structure

The envelope consists of the following fields:

1. **sender**  
   - required  
   - identity of the sender (NZ‑0002)

2. **receiver**  
   - optional  
   - identity of the intended receiver  
   - omitted for broadcast messages

3. **message_type**  
   - required  
   - deterministic classification of the message  
   - defined by higher‑level specifications

4. **flow_id**  
   - optional  
   - deterministic identifier for multi‑step flows  
   - must not rely on randomness or timestamps

5. **hop_counter**  
   - required  
   - incremented deterministically by each forwarding node  
   - used for loop prevention

6. **integrity_tag**  
   - required  
   - deterministic integrity check  
   - algorithm‑agnostic and quantum‑resilient  
   - defined in future specifications

---

## 7. Encoding Rules

### 7.1 Field Ordering
Fields must appear in the exact order defined in this specification.

### 7.2 Explicit Values
All fields must be explicitly present, even if empty (except receiver and flow_id).

### 7.3 Deterministic Types
All fields must use deterministic, platform‑agnostic types.

### 7.4 No Implicit Behavior
No field may imply behavior not explicitly defined.

---

## 8. Security Considerations

- The envelope must not expose sensitive information.  
- Integrity tags must be resistant to quantum attacks.  
- Hop counters must prevent routing loops.  
- Flow IDs must not leak internal state.  
- Message types must not enable fingerprinting attacks.  
- Envelope structure must be formally verifiable.

---

## 9. Future Work

- NZ‑0010 Payload Schema Definition  
- NZ‑0023 Quantum‑Resilient Envelope Integrity  
- NZ‑0031 Deterministic Flow ID Format  
- NZ‑0032 Envelope Compression Rules  

---

## 10. References

None.