# NZ-0033: Fixed-Width Metadata Encoding
Version: draft v0  
Status: Active  
Category: Metadata  

## 1. Purpose

This specification defines fixed‑width metadata encoding rules for the NewZone standard.  
Its purpose is to ensure deterministic, timeless, and formally verifiable encoding of metadata, compatible with payload encoding (NZ‑0029) and transport audit trails (NZ‑0030).

---

## 2. Scope

This specification covers:

- fixed‑width encoding rules for metadata fields  
- compatibility with quantum‑resilient identity hash (NZ‑0028)  
- integration with identity graph verification (NZ‑0032)  
- constraints ensuring predictability and formal verifiability  

This specification does **not** define consensus proofs (NZ‑0034).

---

## 3. Terminology

**Metadata Encoding** — deterministic encoding of descriptive data.  
**Fixed‑Width Encoding** — encoding where each field has a predefined, immutable length.  
**Invariant** — condition that must always hold true.  
**Hash Binding** — deterministic association between metadata and identity hash.

---

## 4. Principles

### 4.1 Determinism  
Encoding must be identical across all implementations.

### 4.2 Minimalism  
Only essential metadata fields may be encoded.

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

- `metadata_header` → 64 bits  
- `metadata_type` → 16 bits  
- `metadata_length` → 32 bits  
- `metadata_checksum` → 256 bits (NZ‑0028 hash)  
- `metadata_data` → fixed‑width blocks (multiples of 256 bits)

### 6.2 Lexicographic Ordering  
Fields must be encoded in strict lexicographic order by field name.

### 6.3 No Optional Fields  
All fields must be present in every encoding.

### 6.4 No Header Compression  
Only metadata data may be compressed, never headers.

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

- preconditions (valid metadata type, valid length)  
- postconditions (deterministic fixed‑width encoding)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of encoding, collision resistance)  

Compatible with NZ‑0008.

---

## 9. Security Considerations

- Malicious nodes must not influence metadata widths.  
- Encoding must preserve hash integrity.  
- Deterministic rules must prevent manipulation.  
- Encoding must be formally verifiable.

---

## 10. Future Work

- NZ‑0034 Deterministic Consensus Proofs  
- NZ‑0035 Stateless Transport Rollback Model  
- NZ‑0036 Identity Graph Compression  
- NZ‑0037 Metadata Integrity Proofs  

---

## 11. References

None.