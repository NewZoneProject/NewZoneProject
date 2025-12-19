# NZ-0025: Fixed-Width Transport Encoding
Version: draft v0  
Status: Active  
Category: Transport  

## 1. Purpose

This specification defines the fixed‑width transport encoding used in the NewZone standard.  
Its purpose is to ensure deterministic, timeless, and formally verifiable encoding of transport envelopes, sessions, and flows without relying on variable‑length or adaptive formats.

---

## 2. Scope

This specification covers:

- fixed‑width encoding rules for transport envelopes (NZ‑0021)  
- fixed‑width encoding rules for sessions (NZ‑0022)  
- fixed‑width encoding rules for flows (NZ‑0023)  
- compatibility with quantum‑resilient transport hash (NZ‑0024)  

This specification does **not** define integrity proofs (NZ‑0026).

---

## 3. Terminology

**Fixed‑Width Encoding** — deterministic encoding where each field has a predefined, immutable length.  
**Transport Envelope** — container defined in NZ‑0021.  
**Session** — deterministic association defined in NZ‑0022.  
**Flow** — stateless control unit defined in NZ‑0023.  
**Hash Output** — 256‑bit deterministic value defined in NZ‑0024.

---

## 4. Principles

### 4.1 Determinism  
Encoding must be identical across all implementations.

### 4.2 Minimalism  
Only essential fields may be encoded.

### 4.3 Predictability  
Encoding must be transparent and reproducible.

### 4.4 Formal Verifiability  
All rules must be expressible in formal logic.

### 4.5 Quantum Resilience  
Encoding must preserve hash integrity against quantum attacks.

### 4.6 Independence  
Encoding must not depend on time, randomness, or external state.

---

## 5. Design Constraints

1. No variable‑length fields.  
2. No optional fields.  
3. No adaptive compression.  
4. No environment‑dependent metadata.  
5. All encoding rules must be deterministic and stable.  
6. Encoding must be forward‑compatible for decades.

---

## 6. Encoding Rules

### 6.1 Field Widths

- `transport_version` → 16 bits  
- `transport_flags` → 16 bits  
- `source_identity` → 256 bits (NZ‑0002 identity hash)  
- `destination_identity` → 256 bits (NZ‑0002 identity hash)  
- `flow_id` → 256 bits (NZ‑0024 hash)  
- `payload_type` → 16 bits  
- `payload_length` → 32 bits  

### 6.2 Lexicographic Ordering  
Fields must be encoded in strict lexicographic order by field name.

### 6.3 No Optional Fields  
All fields must be present in every encoding.

### 6.4 No Header Compression  
Only payload may be compressed, never headers.

---

## 7. Forbidden Mechanisms

Encoding must **never** include:

- variable‑length fields  
- optional fields  
- adaptive compression  
- environment‑dependent metadata  
- dynamic negotiation  

---

## 8. Formal Verification Requirements

Encoding must define:

- preconditions (valid identities, valid payload type)  
- postconditions (deterministic fixed‑width encoding)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of encoding)  

Compatible with NZ‑0008.

---

## 9. Security Considerations

- Malicious nodes must not influence encoding widths.  
- Encoding must preserve hash integrity.  
- Deterministic rules must prevent manipulation.  
- Encoding must be formally verifiable.

---

## 10. Future Work

- NZ‑0026 Deterministic Session Integrity Proofs  
- NZ‑0027 Stateless Flow Verification Model  
- NZ‑0028 Quantum‑Resilient Identity Hash  
- NZ‑0029 Fixed‑Width Payload Encoding  

---

## 11. References

None.