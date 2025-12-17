# NZ-0012: Routing Table Compression
Version: draft v0  
Status: Active  
Category: Core  

## 1. Purpose

This specification defines deterministic routing table compression rules for the NewZone standard.  
Its purpose is to minimize storage requirements, reduce redundancy, and ensure that routing tables remain durable, portable, and formally verifiable across all implementations.

---

## 2. Scope

This specification covers:

- deterministic compression rules  
- table reduction strategies  
- constraints ensuring predictability and formal verifiability  
- terminology used across routing‑related specifications  

This specification does **not** define routing discovery, path selection, or transport mechanisms.

---

## 3. Terminology

**Routing Table** — a deterministic mapping of destination → next hop.  
**Compressed Table** — a reduced representation of a routing table.  
**Prefix Group** — a deterministic grouping of identities with shared structural properties.  
**Identity Ordering** — deterministic ordering of node identities (NZ‑0002).  
**Lossless Compression** — compression that preserves all routing semantics.

---

## 4. Principles

### 4.1 Determinism  
Compression must produce identical results for identical inputs.

### 4.2 Minimalism  
Only essential routing information may be preserved.

### 4.3 Losslessness  
Compression must not alter routing semantics.

### 4.4 Formal Verifiability  
Compression rules must be expressible in formal logic.

### 4.5 Quantum Resilience  
Compression must not rely on cryptographic shortcuts vulnerable to quantum attacks.

### 4.6 Independence  
Compression must not depend on time, randomness, or external state.

---

## 5. Design Constraints

1. No probabilistic or heuristic compression.  
2. No timestamps or time‑based behavior.  
3. No randomness or entropy sources.  
4. No environment‑dependent metadata.  
5. No reliance on synchronized clocks.  
6. All compression rules must be deterministic.  
7. Compression must be reversible (lossless).  
8. Compression must be stable across decades.

---

## 6. Compression Rules

Routing table compression proceeds in the following deterministic order:

### 6.1 Rule 1 — Remove Redundant Entries  
If multiple entries map to the same next hop and share a common identity prefix, group them into a prefix group.

### 6.2 Rule 2 — Collapse Prefix Groups  
Replace grouped entries with a single prefix entry:

- prefix → next hop  
- prefix must be deterministic and minimal  
- prefix must not overlap with other prefixes

### 6.3 Rule 3 — Remove Dominated Entries  
If an entry is fully covered by a prefix group, remove it.

### 6.4 Rule 4 — Deterministic Ordering  
Compressed entries must be ordered lexicographically by:

1. prefix  
2. next hop identity  

### 6.5 Rule 5 — Stable Grouping  
Prefix groups must be stable across implementations:

- no dynamic thresholds  
- no heuristic grouping  
- no probabilistic clustering  

### 6.6 Rule 6 — Identity‑Aligned Compression  
Compression must align with identity structure defined in NZ‑0002.

---

## 7. Reversibility Requirements

A compressed routing table must allow:

- deterministic reconstruction of the full table  
- deterministic expansion of prefix groups  
- deterministic validation of coverage  

Reconstruction must not require external metadata.

---

## 8. Formal Verification Requirements

Compression must define:

- preconditions (valid routing table)  
- postconditions (lossless compressed table)  
- invariants (no ambiguity, no overlap)  
- proof obligations (reversibility, determinism)  

All rules must be compatible with NZ‑0008.

---

## 9. Security Considerations

- Compression must assume adversarial environments.  
- Malicious nodes must not influence prefix grouping.  
- Identity spoofing must be detectable by higher‑level specifications.  
- Compression must not leak sensitive information.  
- Deterministic rules must prevent routing manipulation.

---

## 10. Future Work

- NZ‑0041 Prefix Group Integrity Format  
- NZ‑0042 Deterministic Table Expansion Rules  
- NZ‑0043 Multi‑Layer Compression Model  
- NZ‑0044 Formal Compression Proofs  

---

## 11. References

None.