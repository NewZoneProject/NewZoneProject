# NZ-0036: Identity Graph Compression
Version: draft v0  
Status: Active  
Category: Identity  

## 1. Purpose

This specification defines deterministic compression rules for identity graphs in the NewZone standard.  
Its purpose is to reduce storage and transmission overhead while preserving deterministic verification and quantum‑resilient integrity.

---

## 2. Scope

This specification covers:

- deterministic compression of identity graph structures  
- compatibility with identity graph verification (NZ‑0032)  
- integration with quantum‑resilient identity hash (NZ‑0028)  
- constraints ensuring predictability and formal verifiability  

This specification does **not** define metadata integrity proofs (NZ‑0037).

---

## 3. Terminology

**Identity Graph** — deterministic graph of identities and their relationships.  
**Compression** — deterministic reduction of graph representation size.  
**Invariant** — condition that must always hold true.  
**Hash Binding** — deterministic association between compressed graph and identity hash.

---

## 4. Principles

### 4.1 Determinism  
Compression must be identical across all implementations.

### 4.2 Minimalism  
Only essential graph data may be preserved.

### 4.3 Predictability  
Compression must be transparent and reproducible.

### 4.4 Formal Verifiability  
All rules must be expressible in formal logic.

### 4.5 Quantum Resilience  
Compression must preserve hash integrity against quantum attacks.

### 4.6 Independence  
Compression must not depend on time, randomness, or external state.

---

## 5. Design Constraints

1. No probabilistic compression.  
2. No time‑based validation.  
3. No adaptive or environment‑dependent metadata.  
4. No dynamic negotiation.  
5. All compression rules must be deterministic and stable.  
6. Compression must be forward‑compatible for decades.

---

## 6. Compression Rules

### 6.1 Node Ordering  
Nodes must be ordered lexicographically by identity hash.

### 6.2 Edge Ordering  
Edges must be ordered lexicographically by source and target identity.

### 6.3 Fixed‑Width Encoding  
All compressed graph fields must use fixed‑width encoding (NZ‑0033).

### 6.4 No Optional Fields  
All nodes and edges must be present in compressed representation.

### 6.5 Hash Binding  
Compressed graph must bind to quantum‑resilient identity hash (NZ‑0028).

---

## 7. Forbidden Mechanisms

Compression must **never** include:

- variable‑length fields  
- optional fields  
- adaptive compression  
- environment‑dependent metadata  
- dynamic negotiation  

---

## 8. Formal Verification Requirements

Compression must define:

- preconditions (valid identity graph, valid encoding parameters)  
- postconditions (deterministic compressed graph output)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness, collision resistance)  

Compatible with NZ‑0008.

---

## 9. Security Considerations

- Malicious nodes must not influence compression outputs.  
- Compression must preserve hash integrity.  
- Deterministic rules must prevent manipulation.  
- Compression must be formally verifiable.

---

## 10. Future Work

- NZ‑0037 Metadata Integrity Proofs  
- NZ‑0038 Deterministic Consensus Rollback  
- NZ‑0039 Stateless Transport Replay Model  
- NZ‑0040 Identity Graph Integrity Proofs  

---

## 11. References

None.