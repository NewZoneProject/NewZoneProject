# NZ-0029: Fixed-Width Payload Encoding
Version: draft v0  
Status: Active  
Category: Transport  

## 1. Purpose

This specification defines fixed‑width payload encoding rules for the NewZone standard.  
Its purpose is to ensure deterministic, timeless, and formally verifiable encoding of payload data, compatible with transport envelopes (NZ‑0021), sessions (NZ‑0022), flows (NZ‑0023), and fixed‑width transport encoding (NZ‑0025).

---

## 2. Scope

This specification covers:

- fixed‑width encoding rules for payload data  
- compatibility with quantum‑resilient transport hash (NZ‑0024)  
- integration with session integrity proofs (NZ‑0026) and flow verification (NZ‑0027)  
- constraints ensuring predictability and formal verifiability  

This specification does **not** define transport audit trails (NZ‑0030).

---

## 3. Terminology

**Payload Encoding** — deterministic encoding of application data.  
**Fixed‑Width Encoding** — encoding where each field has a predefined, immutable length.  
**Invariant** — condition that must always hold true.  
**Hash Binding** — deterministic association between payload and transport hash.

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

- `payload_header` → 128 bits  
- `payload_type` → 16 bits  
- `payload_length` → 32 bits  
- `payload_checksum` → 256 bits (NZ‑0024 hash)  
- `payload_data` → fixed‑width blocks (multiples of 512 bits)

### 6.2 Lexicographic Ordering  
Fields must be encoded in strict lexicographic order by field name.

### 6.3 No Optional Fields  
All fields must be present in every encoding.

### 6.4 No Header Compression  
Only payload data may be compressed, never headers.

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

- preconditions (valid payload type, valid length)  
- postconditions (deterministic fixed‑width encoding)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of encoding, collision resistance)  

Compatible with NZ‑0008.

---

## 9. Security Considerations

- Malicious nodes must not influence payload widths.  
- Encoding must preserve hash integrity.  
- Deterministic rules must prevent manipulation.  
- Encoding must be formally verifiable.

---

## 10. Future Work

- NZ‑0030 Deterministic Transport Audit Trails  
- NZ‑0031 Stateless Transport Recovery Model  
- NZ‑0032 Identity Graph Verification  
- NZ‑0033 Fixed‑Width Metadata Encoding  

---

## 11. References

None.